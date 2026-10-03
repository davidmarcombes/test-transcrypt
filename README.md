# Transcrypt set up test

## Linux

Transcript installation

Download
```sh
git clone https://github.com/elasticdog/transcrypt.git
```

Add to pass via symbolic link
```sh
cd transcrypt/
sudo ln -s ${PWD}/transcrypt /usr/local/bin/transcrypt
```

## Windows

Windows installation require git for windows to be installed and access to git bash


Download in the same way as above

**Copy** to ```:usr:bin/```

+ Open a git bash prompt with admin privilege
+ Use cp to copy
+ Check transcrypt in path

```sh
cp /c/work/repos/transcrypt/transcrypt /usr/bin/transcrypt
transcrypt --version
``` 

Assuming you have clone the transcrypt repo in ```C:/work/repos/transcrypt```


## Initialising repo

Go to the root of the repo
```sh
cd test-transcrypt/
```

Let transcrypt interactive guide you
```sh
transcrypt
```

Interaction look like so
```
Encrypt using which cipher? [aes-256-cbc] 
Generate a random password? [Y/n] 
Password: ThisMoodNeedsARestart

Repository metadata:

  GIT_WORK_TREE:  /mnt/data/code/test-transcrypt
  GIT_DIR:        /mnt/data/code/test-transcrypt/.git
  GIT_ATTRIBUTES: /mnt/data/code/test-transcrypt/.gitattributes

The following configuration will be saved:

  CONTEXT:  default
  CIPHER:   aes-256-cbc
  PASSWORD: ThisMoodNeedsARestart

Does this look correct? [Y/n] 

The repository has been successfully configured by transcrypt.
```

**In real situation never share the password in git, use a secondary secure message system**

## Adding a sensitive file

```sh
touch sensitive.py 
transcrypt --add sensitive.py 
```

a line like this has been added to ```.gitattributes```

```
sensitive.py  filter=crypt diff=crypt merge=crypt
```

Then you just need to add th files to git and commit

```
git add .gitattributes sensitive.py 
$ git commit -m 'Adding a secret file'
```

## Useful commands

```
transcrypt --list
```

```
transcrypt --show-raw sensitive_file
```

## Initialise clone

Owner side run 
```
transcrypt --display
```

To get a summary, **do not keep in plain text in git, exchange securely**

```
The current repository was configured using transcrypt version 2.3.3-pre
and has the following configuration:

  GIT_WORK_TREE:  /mnt/data/code/test-transcrypt
  GIT_DIR:        /mnt/data/code/test-transcrypt/.git
  GIT_ATTRIBUTES: /mnt/data/code/test-transcrypt/.gitattributes

  CONTEXT:  default
  CIPHER:   aes-256-cbc
  PASSWORD: ThisMoodNeedsARestart

Copy and paste the following command to initialize a cloned repository:

  transcrypt -c aes-256-cbc -p 'ThisMoodNeedsARestart'
```

On clone side just execute the following on a clean repo clone

```
transcrypt -c aes-256-cbc -p 'ThisMoodNeedsARestart'
```

(If running on windows you have to do this under git bash)

The prompt answer should look like

```
Repository metadata:

  GIT_WORK_TREE:  E:/Code/test-transcrypt
  GIT_DIR:        /e/code/test-transcrypt/.git
  GIT_ATTRIBUTES: E:/Code/test-transcrypt/.gitattributes

The following configuration will be saved:

  CONTEXT:  default
  CIPHER:   aes-256-cbc
  PASSWORD: ThisMoodNeedsARestart

Does this look correct? [Y/n]

The repository has been successfully configured by transcrypt.
```

And the crypted files should now be visible
