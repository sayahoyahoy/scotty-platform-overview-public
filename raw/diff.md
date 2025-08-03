# Scotty Patch Diff
## Overview
The Scotty Patch Diff library solves the complex challenge of three-way data merging, tailored specifically for scenarios where traditional line-by-line document merging falls short.
This necessity arises from the unique constraint in our system: the `mine` data may not always be complete due to its dependency on a user-bound validation schema. Users, based on their permissions and additional schema-related checks, might not have access to the full document, leaving certain data elements confidential.

In a standard three-way merge at the line level, the outcome includes context lines around changes, which are essential for positioning and conflict resolution. However, this method risks exposing sensitive data. This lib leverages our knowledge of the document schema, allowing us to merge at the granular level of individual schema properties. We identify changes and then diff them each against the corresponding elements in the `base` and `theirs` versions.

**The true challenge arises with arrays.**
A conflict within an array item could potentially expose secret fields. To prevent this, we've implemented a custom array merge processing. This involves calculating the movements, deletions, and additions of elements. Before processing the arrays for further changes, we update elements where properties have changed and then exclude them from the subsequent array processing. Next, we convert the data to hashes and perform a 3-way merge on these placeholders. On the resulting merge will we calculate the movements in the array. This approach ensures that no data, that a user modifying the document isn't authorized to see, gets exposed – even in scenarios where conflicts arise.

## Functions
### getChanges
Compares three objects - mine, theirs, and base - and returns a list of changes.

#### Parameters
    mine: unknown
    theirs: unknown
    base: unknown
    definitionName: string
    queryDefinitions: QuerySchema['definitions']

#### Returns
    An array of Changes objects, each representing a specific change.

    interface Changes {
        path: string,
        type: string,
        conflicts?: boolean,
        diffResult: ParsedDiff,
        changes?: ArrayChanges
    }

### applyChanges
Applies changes to the base version of the data.

#### Parameters
    base: unknown
    changes: Changes[]
    take: 'mine' | 'theirs'
#### Returns
    The modified version of base with the applied changes.
