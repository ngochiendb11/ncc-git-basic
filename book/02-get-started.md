- [Getting Started](#getting-started)
  - [1. Installation](#1-installation)
  - [2. First-Time Git Setup](#2-first-time-git-setup)
    - [Your Identity](#your-identity)
    - [Alias](#alias)
  - [3. `git init`](#3-git-init)
  - [4. `git clone`](#4-git-clone)

# Getting Started

## 1. Installation

Các bạn tham khảo hướng dẫn cài đặt git trên documents nha! Mình có để [link](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) đây nha!

## 2. First-Time Git Setup

### Your Identity

```
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```

### Alias

```
git config --global alias.co checkout

git config --global alias.br branch

git config --global alias.ci commit

git config --global alias.st status
```

View all config:

```
git config --list
```

## 3. `git init`

Tác dụng : Khởi tạo 1 git repository 1 project mới hoặc đã có.

Cách dùng: `git init` trong thư mục gốc của dự án.

## 4. `git clone`

Tác dụng: Copy 1 git repository từ remote source.

Cách dùng: git clone <:clone git url:>
