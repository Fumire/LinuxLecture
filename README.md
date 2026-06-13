# LinuxLecture

LinuxLecture is a beginner-friendly Linux lecture deck written with LaTeX
Beamer. It introduces students to the Linux shell, basic file operations, text
editing with Vim, input/output redirection, downloads and archives, Unix file
permissions, process control, and basic Slurm job scheduling.

The repository includes both the editable source (`linux.tex`) and a generated
PDF (`linux.pdf`) so that instructors can either present the existing slides or
modify and rebuild the deck.

## Table of Contents

- [Audience](#audience)
- [Repository Contents](#repository-contents)
- [Quick Start](#quick-start)
- [Build Requirements](#build-requirements)
- [Lecture Outline](#lecture-outline)
  - [1. Linux and Ubuntu](#1-linux-and-ubuntu)
  - [2. Basic Linux Commands](#2-basic-linux-commands)
  - [3. Editing Files with Vim](#3-editing-files-with-vim)
  - [4. Input and Output Redirection](#4-input-and-output-redirection)
  - [5. Downloading and Archives](#5-downloading-and-archives)
  - [6. User Permissions](#6-user-permissions)
  - [7. Process Control](#7-process-control)
  - [8. Slurm Job Scheduling](#8-slurm-job-scheduling)
- [Suggested Student Workflow](#suggested-student-workflow)
- [Safety Notes](#safety-notes)
- [Customizing the Lecture](#customizing-the-lecture)
- [License](#license)

## Audience

This material is intended for first-time Linux users in a classroom, lab, or
shared server environment. The examples assume that learners can open a Linux
shell through one of these setups:

- Ubuntu LTS, Windows Subsystem for Linux, or another Linux desktop
- A remote Linux server reached through SSH
- A course-provided shell environment
- A terminal running `bash` or `zsh`

The commands are intentionally simple and use common tools that are available on
most Linux systems.

## Repository Contents

| Path | Description |
| --- | --- |
| `linux.tex` | Main LaTeX Beamer source for the lecture slides. |
| `linux.pdf` | Prebuilt PDF version of the lecture. |
| `figures/` | Images and screenshots used by the slides. |
| `LICENSE` | MIT license for the repository. |
| `README.md` | This project overview and usage guide. |

## Quick Start

To use the lecture immediately, open `linux.pdf` in any PDF viewer.

To edit the lecture, modify `linux.tex` and rebuild the PDF:

```sh
latexmk -pdf linux.tex
```

If `latexmk` is not available, you can use `pdflatex` directly:

```sh
pdflatex linux.tex
pdflatex linux.tex
```

Running `pdflatex` twice helps LaTeX update cross-references and the table of
contents.

## Build Requirements

You need a LaTeX distribution that includes Beamer and common graphics support.

Recommended options:

- macOS: MacTeX
- Ubuntu/Debian: `texlive`, `texlive-latex-extra`, and `latexmk`
- Windows: TeX Live, MiKTeX, or WSL with TeX Live

On Ubuntu or Debian-based systems, a typical setup is:

```sh
sudo apt update
sudo apt install texlive texlive-latex-extra latexmk
```

## Lecture Outline

The deck is organized as a practical introduction. Each topic starts with the
reason the command matters, then shows small commands that students can type in a
terminal.

### 1. Linux and Ubuntu

This section introduces Linux as an open source operating system family and
Ubuntu as a common beginner-friendly Linux distribution. It gives students the
context they need before they begin typing commands.

### 2. Basic Linux Commands

Students learn how to move around the filesystem and manage files:

- `pwd` prints the current working directory.
- `ls` lists files and directories.
- `mkdir` creates a new directory.
- `cd` changes the current directory.
- Tab completion helps complete commands and paths.
- `man` and `--help` provide command documentation.
- `touch` creates an empty file or updates a file timestamp.
- `mv` moves or renames files.
- `cp` copies files.
- `rm` removes files and directories.
- `sudo` runs commands with elevated privileges when allowed.

This part also explains important directory concepts such as the home directory,
`.` for the current directory, and `..` for the parent directory.

### 3. Editing Files with Vim

The editor section introduces common terminal editors and uses Vim as the main
example because it is widely available on Linux servers. Students learn the basic
Vim workflow:

1. Open a file with `vim filename`.
2. Press `i` to enter insert mode.
3. Edit the file.
4. Press `Esc` to return to normal mode.
5. Save with `:w`.
6. Quit with `:q`.

The deck also points students to `vimtutor` for optional practice.

### 4. Input and Output Redirection

This section explains how commands read input and write output:

- `cat` prints file contents.
- `>` writes output to a file and overwrites existing content.
- `>>` appends output to a file.
- `<` reads input from a file.
- `1>` redirects standard output.
- `2>` redirects standard error.
- `more` and `less` display longer files page by page.
- `|` pipes the output of one command into another command.

These ideas are important because many Linux workflows are built by connecting
small commands together.

### 5. Downloading and Archives

Students learn two common download tools:

- `curl` for fetching URLs and optionally saving output with `-o`
- `wget` for downloading files directly

The section also covers compressed files and archives:

- `gzip` compresses or decompresses single files.
- `gzip -k` keeps the original file while compressing.
- `tar -xzf file.tar.gz` extracts a compressed tar archive.

These examples are useful for downloading lab files, source code, datasets, or
course materials.

### 6. User Permissions

The permissions section explains how to inspect and change file permissions:

- `ls -al` shows file modes, owners, groups, and hidden files.
- `chmod` changes read, write, and execute permissions.
- Numeric permissions such as `660` and `770` are introduced.
- Symbolic forms such as `chmod g=rwx file` and `chmod +x file` are shown.
- `chown` changes file ownership.

This topic is especially important on shared servers, where incorrect
permissions can expose private files or prevent collaborators from using shared
work.

### 7. Process Control

Students learn how to handle long-running commands:

- `Ctrl-C` sends an interrupt signal to stop a foreground process.
- `&` starts a command in the background.
- `jobs` lists background jobs in the current shell.
- `kill %number` stops a background job by job number.
- `kill PID` stops a process by process ID.
- `nohup` keeps a command running after an SSH session disconnects.
- `screen` lets users detach and return to terminal sessions.

These commands help students work safely on remote servers.

### 8. Slurm Job Scheduling

The final section introduces Slurm for shared clusters. Students learn what a
job scheduler does and how to submit, inspect, and cancel jobs:

- Write a shell script with `#SBATCH` resource options.
- Submit a job with `sbatch`.
- Choose stdout and stderr log files with `--output` and `--error`.
- Check jobs with `squeue -u $USER`.
- Cancel a job with `scancel JOBID`.
- Cancel all of a user's jobs with `scancel -u $USER`.

The Slurm examples are intentionally small and should be adjusted to match the
policies of the cluster or classroom server where the lecture is taught.

## Suggested Student Workflow

For a hands-on lab, students can create a clean practice directory before trying
the examples:

```sh
mkdir -p ~/linux-lab
cd ~/linux-lab
pwd
```

Keeping practice files in one directory makes it easier to experiment without
mixing lab files with personal files.

## Safety Notes

- Read each command before pressing Enter.
- Be careful with `rm`; removed files may not be recoverable.
- Be careful with `sudo`; it can change system files or affect other users.
- On shared machines, avoid running heavy jobs directly in the login shell.
- Follow local Slurm, storage, and server policies when working on a cluster.

## Customizing the Lecture

Instructors can update `linux.tex` to match a specific course environment. Common
customizations include:

- Replacing screenshots in `figures/`
- Updating SSH, server, or cluster examples
- Changing Slurm resource examples such as time, CPU, memory, partition, or GPU
  options
- Adding local software installation instructions
- Translating explanations or adding course-specific exercises

After editing, rebuild `linux.pdf` and review the slides to make sure images,
line breaks, and command examples still fit well.

## License

This repository is released under the MIT License. See `LICENSE` for the full
license text.
