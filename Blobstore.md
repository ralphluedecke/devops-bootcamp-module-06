# Nexus Blob Store
- is a storage area to store all the assets (local or remote)
- Settings>Repository>Blob Stores

## Table of Contents

- [permutations](#permutations)
- [types](#types)
- [states](#states)
- [file system](#file-system)
- [consider](#consider)
- [decide](#decide)

## permutations
- default
- manual created

## types
- File - File system-based storage
- Group - combine several blob stores
- AWS S3
- Azure
- Google Cloud

## states
- started
- failed

## file system
### install and configurations
```bash
/opt/sonatype-work/nexus3/blobs
```
### data
```bash
/opt/sonatype-work/nexus3/blobs/<NAME_OF_BLOBSTORE>/content
```
organized by data (2026/07/20/16/52/00)

## consider
- Blob Stores can't be modified!
- Blob Store used by a repository can't be deleted

## decide
- How many blob stores will you create?
- With which sizes?
- Which ones you'll use for which repos?
- How much space for each repo?

## assign blob store
When creating a repo go to
```bash
Settings>Repository>assign Blob Store 
```