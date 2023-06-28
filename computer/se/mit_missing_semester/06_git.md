# MIT Missing Semester 分析笔记

## [6 Version Control (Git)][1]

- Snapshots
  - A snapshot is the top-level tree that is being tracked.
  - Git calls these snapshots "commit"s.

- History
  - A history is a directed acyclic graph (DAG) of snapshots.

- Data model, as pseudocode

  ```text
  // a file is a bunch of bytes
  type blob = array<byte>

  // a directory contains named files and directories
  type tree = map<string, tree | blob>

  // a commit has parents, metadata, and the top-level tree
  type commit = struct {
      parents: array<commit>
      author: string
      message: string
      snapshot: tree
  }
  ```

- An “object” is a blob, tree, or commit:

  ```text
  type object = blob | tree | commit
  ```

- All objects are content-addressed by their SHA-1 hash.

  ```text
  objects = map<string, object>

  def store(object):
      id = sha1(object)
      objects[id] = object

  def load(id):
      return objects[id]
    ```
  
- Check the contents addressed by a SHA-1 hash.

  ```text
  git cat-file -p 503c68c8b1c372bb9ed2c672c187d9ef07c9b512
  ```

- References are pointers to commits.

  ```text
  references = map<string, string>

  def update_reference(name, id):
      references[name] = id

  def read_reference(name):
      return references[name]

  def load_reference(name_or_id):
      if name_or_id in references:
          return load(references[name_or_id])
      else:
          return load(name_or_id)
  ```

- A Git repository is the data objects and references.


  [1]: https://missing.csail.mit.edu/2020/version-control/
