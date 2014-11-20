# rw-ratio

rw-ratio is a Perl script that helps quantify the number of reads and writes in a MySQL database, as well as the deltas of reads, writes and ratios of reads to writes. It uses a vmstat-style output (one line of TAB-separated values.)

## Usage

### Syntax
rw-ratio --host=host --user=user [--password=password --port=port --sleep=sleep]

### Details
OPTIONS

* --host The hostname of IP address of the database server to connect to.
* --port The port number of the database server to connect to. It defaults to 3306.
* --user The username to connect as.
* --password The password to connect with. If not supplied on the command line, you will be prompted for it.
* --sleep The number of seconds to sleep between each sample. It defaults to 300.
* --help This manual page. Full docs are availabe in the POD (perldoc rw-ratio).

## Output

Each line looks like:

> Time: 1253902509 Interval: 10 R: 59 dR: 59 W: 17 dW: 17 dR/dW: 3.47 R/W: 3.47

Fields
* _Time_ The timestamp, expressed as a UNIX epoch, of the sample.
* _Interval_ The number of seconds between the previous sample and the current sample.
* _R_ The total number of database reads.
* _dR_ The delta of reads between the previous sample and the current sample.
* _W_ The total number of database writes.
* _dW_ The delta of writes between the previous sample and the current sample.
* _dR/dW_ The ratio of reads to writes, calculated using the current deltas
* _R/W_ The ratio of reads to writes, calculated using the totals

## Notes
The deltas can be disregarded in the first line of output since there are no previous counters to compare to. Two SQL statements count as both read and write statements: INSERT ... SELECT; and REPLACE ... SELECT; so are, thus, counted twice.

