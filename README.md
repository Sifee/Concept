# Concept

(READ-ONLY) The concepts of Sifee.

## 0. Definitions

Sifee is a scalable, disturbed file-system.

It's built on top of a blockchain.

## 1. Architecture

Sifee has three parts:

### 1.0 FileTree

A FileTree is a data structure for storing file names, locations and other informations.

It is a tiny data structure and will be managed as a blockchain.

### 1.1 DataPool and DataLake

A DataPool is a directory for Sifee to store the real data.

A DataLake is a collection of several DataPools.

In a DataLake, data are called objects.

In the FileTree, a file will be pointed to an object.

DataLake uses CoW (Copy on Write) model.

### 1.2 DataLayer

DataLayer is similar to layers in AUFS (Advanced Union File-System).

But DataLayers in Sifee are for data recovering and commit-locks.

Every operations on each file will be operated on the top-layer (with a CoW model), and when the user asks to create a new commit, the top-layer will become a layer which is similar to image-layers in AUFS, and a new top-layer will be created.

Each layer owns its own FileTree.

### 1.3 CacheLayer

There're 2 types of CacheLayers: DiskCache and MemoryCache.

As you see, DiskCache caches files in dedicated files on hard-drives, and MemoryCache caches files as a stream in memory.
