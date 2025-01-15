# Cracken

## Usage Info


```
$ cracken --help
Cracken v1.0.0 - a fast password wordlist generator 

USAGE:
    cracken [SUBCOMMAND]

FLAGS:
    -h, --help       Prints help information
    -V, --version    Prints version information

SUBCOMMANDS:
    generate    (default) - Generates newline separated words according to given mask and wordlist files
    create      Create a new smartlist from input file(s)
    entropy     
                Computes the estimated entropy of password or password file.
                The entropy of a password is the log2(len(keyspace)) of the password.
                
                There are two types of keyspace size estimations:
                  * mask - keyspace of each char (digit=10, lowercase=26...).
                  * hybrid - finding minimal split into subwords and charsets.


For specific subcommand help run: cracken <subcommand> --help


Example Usage:

  ## Generate Subcommand Examples:

  # all digits from 00000000 to 99999999
  cracken ?d?d?d?d?d?d?d?d

  # all digits from 0 to 99999999
  cracken -m 1 ?d?d?d?d?d?d?d?d

  # words with pwd prefix - pwd0000 to pwd9999
  cracken pwd?d?d?d?d

  # all passwords of length 8 starting with upper then 6 lowers then digit
  cracken ?u?l?l?l?l?l?l?d

  # same as above, write output to pwds.txt instead of stdout
  cracken -o pwds.txt ?u?l?l?l?l?l?l?d

  # custom charset - all hex values
  cracken -c 0123456789abcdef '?1?1?1?1'

  # 4 custom charsets - the order determines the id of the charset
  cracken -c 01 -c ab -c de -c ef '?1?2?3?4'

  # 4 lowercase chars with years 2000-2019 suffix
  cracken -c 01 '?l?l?l?l20?1?d'

  # starts with firstname from wordlist followed by 4 digits
  cracken -w firstnames.txt '?w1?d?d?d?d'

  # starts with firstname from wordlist with lastname from wordlist ending with symbol
  cracken -w firstnames.txt -w lastnames.txt -c '!@#$' '?w1?w2?1'

  # repeating wordlists multiple times and combining charsets
  cracken -w verbs.txt -w nouns.txt '?w1?w2?w1?w2?w2?d?d?d'


  ## Create Smartlists Subcommand Examples:

  # create smartlist from single file into smart.txt
  cracken create -f rockyou.txt --smartlist smart.txt

  # create smartlist from multiple files with multiple tokenization algorithms
  cracken create -t bpe -t unigram -t wordpiece -f rockyou.txt -f passwords.txt -f wikipedia.txt --smartlist smart.txt

  # create smartlist with minimum subword length of 3 and max numbers-only subwords of size 6
  cracken create -f rockyou.txt --min-word-len 3 --numbers-max-size 6 --smartlist smart.txt


  ## Entropy Subcommand Examples:

  # estimating entropy of a password
  cracken entropy --smartlist vocab.txt 'helloworld123!'

  # estimating entropy of a passwords file with a charset mask entropy (default is hybrid)
  cracken entropy --smartlist vocab.txt -t charset -p passwords.txt

  # estimating the entropy of a passwords file
  cracken entropy --smartlist vocab.txt -p passwords.txt

cracken-v1.0.0 linux-x86_64 compiler: rustc 1.56.1 (59eed8a2a 2021-11-01)
more info at: https://github.com/shmuelamar/cracken
```
