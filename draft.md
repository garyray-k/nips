NIP-??
======

Source Control Context
----------------------

`draft` `optional` `author:garyKrause_`

This NIP defines ways source control (git, etc.) context can be stored using nostr. Git is already decentralized, but the contexts around a git repository are largely centralized (PR comments, issue tracking, releases, etc). With the correct approach a nostr relay could store this context using many of the existing NIPs. This NIP defines a new kind, `kind: ??`, to represent a source control repository. This NIP purposely does not indicate git as a requirement but many of the concepts will be based around git methods of source control. The author hopes that the NIP is flexible enough to accomodate other source control methodologies.

## Definition of a Source Control Event

`kind: ??` uses tag the `b` tag to identify the base repository. The value of this tag SHALL be a list of remote source control repository URLs. These URLs MAY be a nostr relay URL or a traditional repository URL. The first URL in this list SHALL be considered the "default" repository URL for the context.

The `content` of a Source Control Event MAY contain a text description of the event or other information about the repository.
    
```json
{
    ...
  "kind": ??,
  "tags": [
    ["b", <repository url>, <repository url>, ...],
  ],
  "content": <arbitrary string>,
  ...
```

A relay MAY host the repository along side it's nostr database which can be discovered using a standard `REQ` message filtering for `kind: ??`.

### Merge Requests

A source control event MAY contain an `m` tag indicating the event is specific to a merge request. If present, the `m` tag SHALL define the branch being merged into and the branch being merged in. An event MAY include the URL of the repository being merged from. This could be included when the URL being merged from is not in the `b` tag of the event or for specificity. When creating a merge request, the `content` field MAY contain a justification/explanation for the merge

```json
{
    ...
  "kind": ??,
  "tags": [
    ["b", <repository url>, <repository url>, ...],
    ["m": <branch to be merged into>, <branch to be merged in>, <URL of merging in repository>],
  ],
  "content": <arbitrary string>,
  ...
```

### Issue/Bug Tracking

????