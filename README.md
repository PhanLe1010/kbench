# Benchmark

Various benchmark for storage and Kubernetes.

## FIO

### Deploy in Kubernetes cluster

Start:
```
kubectl apply -f deploy/fio.yaml
```

Result:
```
kubectl logs benchmark-xxxxx
```

Cleanup:
```
kubectl delete -f deploy/fio.yaml
```

See YAML for available options

### Running as a binary locally
Usage:
```
./fio/run.sh <test_target> <output_prefix>
```

Intermediate result will be saved into `<output_prefix>-benchmark.json` and `<output_prefix>-cpu.json`.
The output will be printed out as well as saved into `<output_prefix>.summary`.

#### Example
```
$ export TEST_TARGET=/dev/sdxx
$ export OUTPUT_PREFIX=./fio-results/Samsung_850_PRO_512GB/raw-block
$ sudo ./fio/run.sh $TEST_TARGET $OUTPUT_PREFIX
....
....
=====================
FIO Benchmark Summary
For: ./fio-results/Samsung_850_PRO_512GB/raw-block
=====================

Random Read/Write
IOPS:             97,831  / 87,143
Bandwidth:        546,501 KiB/sec   / 506,343 KiB/sec
Average Latency:  118,385 ns  / 45,925 ns

Sequential Read/Write
IOPS:             106,640 / 105,740
Bandwidth:        548,037 KiB/sec   / 513,163 KiB/sec
Average Latency:  43,137 ns  / 46,133 ns

CPU Idleness: 74%
```

Note: the benchmark for FIO will take about 6 minutes to finish.

### Understanding the result

One thing need to pay extra attention regarding the result, is the CPU Idleness should be at least 40% to guarantee the test doesn't become CPU bound.
