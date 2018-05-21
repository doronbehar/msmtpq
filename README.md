# `msmtpq` - `msmtp` wrapper for queueing mails.

[`msmtp`](http://msmtp.sourceforge.net) is an SMTP client that doesn't support natively queuing mails for sending them later. This script, inspired by scripts contributed to the project (found [here](https://sourceforge.net/p/msmtp/code/ci/master/tree/scripts/)), strives to act like a mature command line application with standard command line arguments, configuration files and environmental variables support.

## Usage

```
Usage: msmtpq [OPTION]...
   -c,--config <FILE>     Use the given configuration file instead of the 
                          default one (/home/doron/.config/msmtpq/default.conf), 
                          can also be set with `$MSMTPQ_CONFIG` 
   -l,--list              List all queued emails. If used with `--verbose`, the 
                          full emails are printed 
   -r,--run               Try to send all the emails in the queue 
   -v,--verbose           Turn on verbose output 
   -n,--dry-run           don't store emails in queue but show only what 
                          actions would have been taken if msmtpq would have run 
                          normally (with or without --run), implies --verbose 
   -h,--help              display help 
```

Other options which should be passed to native `msmtp` are processed as well.

## Configuration

The configuration file, which is basically a shell script which `msmtpq` sources, can have the following variables (default values are shown):

```sh
# the directory in it mails will be stored
QUEUEDIR="${HOME}/.msmtpq"
# the date format with which files will be stored in the queue directory
DATEFORMAT="%Y-%m-%d-%H.%M.%S"
# The lock file which will be used to track if another instance of the script
# runs in conjunction to the current instance
LOCKFILE="${QUEUEDIR}/.lock"
# The umask which will be used when creating files in the queue directory
UMASK=077
```

Every variable used in the configuration file can be overridden using environmental variables if you use `--config /dev/null`.
