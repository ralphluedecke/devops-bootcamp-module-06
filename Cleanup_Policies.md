# Cleanup Policies

###  Table of Contents

- [create](#create)
- [attach policy to repo](#attach-policy-to-repo)
- [configure cleanup policy](#configure-cleanup-policy)
- [create new task for compacting the blob store](#create-new-task-for-compacting-the-blob-store)
- [test with manual execution](#test-with-manual-execution)

## create
```bash
Settings>Repository>Cleanup Policies
```
- choose format, Release Type
- Cleanup Criteria (age,usage, asset name matcher)

## attach policy to repo
- choose repo
- cleanup - Cleanup Policy - search and apply

## configure cleanup policy
```bash
Settings>System>Taskspolicy
```
shows list of tasks

# create new task for compacting the blob store
- choose "Admin - Compact blob store"
- give name
- choose blob store 
- choose frequency
- choose date and time

# test with manual execution
- execute "cleanup unused maven2 blobs from nexus" first (marked for deletion blobs will be prepared for deletion)
- press Run at compacting task