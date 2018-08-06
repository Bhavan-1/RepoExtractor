[Developer Chat](https://gitter.im/networknt/microservices-framework-benchmark) |
[Documentation](https://networknt.github.io/microservices-framework-benchmark) |
[Contribution Guide](CONTRIBUTING.md) |


| Framework    | Language   | Max Throughput | Avg Latency | Transfer | 
| ------------ | ---------: | -------------: | ----------: | -------: |
| Go FastHttp  | Go         | 1,396,685.83     | 99.98ms     | 167.83MB |
| Light Java   | Java       | 1,344,512.65     | 2.36ms      | 169.25MB |
| ActFramework | Java       | 945,429.13      | 2.22ms      | 136.15MB |
| Go Iris      | Go         | 828,035.66      | 5.77ms      | 112.92MB |
| Vertx        | Java       | 803,311.31     | 2.37ms       | 98.06MB  |
| Node-uws     | Node/C++   | 589,924.44      |  7.22ms     | 28.69MB  |
| Dotnet       | .Net       | 486,216.93      |  2.93ms     | 57.03MB  |
| Jooby/Undertow | Java     | 362018.07      |  3.95ms     | 47.99MB  |
| SeedStack-Filter | Java   | 343416.33       | 4.41ms      | 51.42MB  |
| Spring Boot Reactor | Java | 243,240.17     | 7.44ms      | 17.86MB  |
| Pippo-Undertow | Java     | 216,254.56     | 9.80ms     | 31.35MB    |
| Spark        | Java       | 194,553.83      |  13.85ms    | 32.47MB  |
| Pippo-Jetty  | Java       | 178,055.45      |  15.66ms    | 26.83MB  |
| Play-Java    | Java       | 177,202.75      |  12.15ms    | 21.80MB  |
| Go HttpRouter | Go        | 171852.31       | 14.12ms     | 21.14MB  |
| Go Http      | Go         | 170,313.02      |  15.01ms    | 20.95MB  |
| JFinal       | Java       | 139,467.87      |  11.89ms    | 29.79MB  |
| Akka-Http    | Java       | 132,157.96  | 12.21ms         | 19.54MB  |
| RatPack      | Java       | 124,700.70     | 13.45ms    | 10.82MB    |
| Pippo-Tomcat   | Java     | 103,948.18     | 23.50ms    | 15.29MB    |
| Bootique + Jetty/Jersey | Java | 65,072.20 | 39.08ms | 11.17MB       |
| SeedStack-Jersey2 | Java  | 52310.11       |  26.88ms     | 11.87MB  |
| Baseio         | Java    | 50,361.98      | 22.20ms    | 6.39MB   |
| NinjaFramework | Java    | 47,956.43      | 55.76ms    | 13.67MB |
| Play 1         | Java    | 44,491.87      | 10.73ms    | 18.75MB  |
| Spring Boot Undertow | Java | 44,260.61 | 38.94ms   | 6.42MB   |
| Nodejs Express | Node     | 42,443.34     | 22.30ms     | 9.31MB   |
| Dropwizard     | Java     | 33,819.90     | 98.78ms     | 3.23MB  |
| Spring Boot Tomcat | Java | 33,086.22 | 82.93ms     | 3.98MB   |
| Node-Loopback  | Node     | 32091.95  | 34.42ms     | 11.51MB  |
| Payra Micro        | Java | 24,768.69 | 118.86ms    | 3.50MB   |
| WildFly Swarm     | Java | 21,541.07  | 59.77ms     | 2.83MB   |


We are using pipeline.lua to generate more requests per second and the pipeline.lua is located
at microservices-framework-benchmark/pipeline.lua.


Here is the light-java server performance with the same command line with other frameworks.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     2.36ms    3.55ms  53.35ms   89.03%
    Req/Sec   338.18k    49.76k  717.09k    76.64%
  Latency Distribution
     50%    1.05ms
     75%    2.48ms
     90%    6.35ms
     99%   17.28ms
  40436304 requests in 30.08s, 4.97GB read
Requests/sec: 1344512.65
Transfer/sec:    169.25MB

```

Here is another test with for light-java to push more requests but some other frameworks get server errors.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 50
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     2.35ms    2.80ms  54.23ms   89.24%
    Req/Sec   550.10k    64.34k    1.22M    74.54%
  Latency Distribution
     50%    1.56ms
     75%    2.87ms
     90%    5.41ms
     99%   22.17ms
  65803650 requests in 30.10s, 6.50GB read
Requests/sec: 2186203.44
Transfer/sec:    221.00MB

```


Here is the spring-boot-tomcat (tomcat embedded) performance.

```
steve@joy:~/tool/wrk$  wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    82.93ms  108.77ms   1.58s    89.45%
    Req/Sec     8.40k     3.68k   22.19k    68.54%
  Latency Distribution
     50%   45.66ms
     75%  101.59ms
     90%  197.72ms
     99%  542.87ms
  995431 requests in 30.09s, 119.79MB read
Requests/sec:  33086.22
Transfer/sec:      3.98MB

```

Here is the spring-boot-undertow (undertow embedded) performance.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    38.94ms   39.29ms 456.82ms   89.28%
    Req/Sec    11.21k     4.97k   28.16k    68.14%
  Latency Distribution
     50%   27.58ms
     75%   49.62ms
     90%   80.73ms
     99%  201.87ms
  1331312 requests in 30.08s, 192.98MB read
Requests/sec:  44260.61
Transfer/sec:      6.42MB
```

Basically, light-4j is 44 times faster than spring-boot with tomcat embedded just
for the raw performance to serve Hello World! 

In order to have a closer comparison, I have created another project spring-boot-undertow with embedded
undertow servlet container (light-java is using undertow core only) and the 
performance is getting a little better. Light-Java is about 33 times faster than spring-boot with undertow embedded.


Upon requests from the community, I have added nodejs and golang examples and here are the testing result.

Node express framework.
To start the server

```
cd node-express
npm install
node server.js

```
The test result.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    22.30ms   24.35ms 592.24ms   49.18%
    Req/Sec    10.70k     0.87k   11.95k    94.82%
  Latency Distribution
     50%   47.94ms
     75%    0.00us
     90%    0.00us
     99%    0.00us
  1274289 requests in 30.02s, 279.51MB read
Requests/sec:  42443.34
Transfer/sec:      9.31MB

```

Go Standard Http

To start the server
```
cd go-http
go run server.go -prefork
```

The testing result.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    15.01ms   15.35ms 180.11ms   87.10%
    Req/Sec    42.80k     5.46k   62.49k    70.58%
  Latency Distribution
     50%   10.03ms
     75%   19.96ms
     90%   34.55ms
     99%   72.99ms
  5123194 requests in 30.08s, 630.28MB read
Requests/sec: 170313.02
Transfer/sec:     20.95MB

```

Go FastHttp

To start the server

```
cd go-fasthttp
go run server.go -prefork

```
The testing result.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    99.98ms  127.12ms 653.72ms   82.12%
    Req/Sec   351.24k    46.23k  525.74k    77.09%
  Latency Distribution
     50%   30.76ms
     75%  175.44ms
     90%  299.14ms
     99%  476.20ms
  41989168 requests in 30.06s, 4.93GB read
Requests/sec: 1396685.83
Transfer/sec:    167.83MB

```

After I post this online, one of spring developers recommended to test against Spring Boot with Reactor
which is Netty based without servlet container. I am very new to this and might miss something and everyone
is welcomed to submit pull request to enhance this project.

Here is the test result.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:3000 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:3000
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     7.44ms   12.88ms 285.71ms   94.23%
    Req/Sec    61.44k    12.25k   88.29k    79.23%
  Latency Distribution
     50%    4.62ms
     75%    8.11ms
     90%   15.03ms
     99%   42.60ms
  7305649 requests in 30.03s, 536.48MB read
Requests/sec: 243240.17
Transfer/sec:     17.86MB

```

Add Spark test case and here is the result. It is much better than most frameworks with servlet containers.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:4567 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:4567
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    13.85ms   30.58ms 687.89ms   96.29%
    Req/Sec    49.10k    16.55k  107.63k    73.41%
  Latency Distribution
     50%    7.28ms
     75%   13.96ms
     90%   24.71ms
     99%  158.21ms
  5855187 requests in 30.10s, 0.95GB read
Requests/sec: 194553.83
Transfer/sec:     32.47MB

```

Add Jooby test case and here is the result. It is better than Spring Boot as it is using Netty directly. 

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    15.57ms   25.97ms 431.00ms   94.64%
    Req/Sec    30.50k     8.66k   77.57k    75.68%
  Latency Distribution
     50%    9.93ms
     75%   16.49ms
     90%   27.27ms
     99%  123.80ms
  3613008 requests in 30.05s, 392.80MB read
Requests/sec: 120232.86
Transfer/sec:     13.07MB

```

@jknack submitted a pull request for Jooby to switch to Undertow instead of Netty and here is the updated result.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    13.22ms   20.07ms 439.26ms   94.77%
    Req/Sec    32.96k     7.71k   52.00k    78.38%
  Latency Distribution
     50%    9.06ms
     75%   14.98ms
     90%   23.88ms
     99%   89.30ms
  3926256 requests in 30.10s, 565.40MB read
Requests/sec: 130458.14
Transfer/sec:     18.79MB

```

@windbender submitted a pull request for Dropwizard and here is the result.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    98.78ms  167.67ms   1.92s    92.91%
    Req/Sec     8.58k     4.26k   24.02k    66.49%
  Latency Distribution
     50%   47.95ms
     75%  103.68ms
     90%  211.24ms
     99%  958.22ms
  1017904 requests in 30.10s, 97.07MB read
Requests/sec:  33819.90
Transfer/sec:      3.23MB

```

@IRus submitted a pull request for Bootique + Jetty/Jersey and here is the result.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    39.08ms   43.35ms 462.13ms   87.33%
    Req/Sec    16.46k     3.79k   31.04k    70.42%
  Latency Distribution
     50%   23.94ms
     75%   49.95ms
     90%   94.78ms
     99%  204.74ms
  1956621 requests in 30.07s, 335.88MB read
Requests/sec:  65072.20
Transfer/sec:     11.17MB
```

@hydra1983 submitted a pull request for RatPack and here is the result.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:5050 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:5050
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    13.45ms   17.27ms 366.84ms   94.60%
    Req/Sec    31.44k     6.39k   48.42k    83.28%
  Latency Distribution
     50%   10.04ms
     75%   16.67ms
     90%   24.47ms
     99%   82.36ms
  3747731 requests in 30.05s, 325.24MB read
Requests/sec: 124700.70
Transfer/sec:     10.82MB

```

@IRus submitted a pull request for WildFly Swarm and here is the result.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    59.77ms   44.97ms 526.38ms   64.92%
    Req/Sec     5.41k     1.43k    9.53k    74.58%
  Latency Distribution
     50%   74.16ms
     75%  162.88ms
     90%    0.00us
     99%    0.00us
  648138 requests in 30.09s, 85.30MB read
Requests/sec:  21541.07
Transfer/sec:      2.83MB
```

@IRus submitted a pull request for Payra-Micro and here is the result.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency   118.86ms  144.34ms   1.77s    88.56%
    Req/Sec     6.29k     2.75k   15.40k    63.00%
  Latency Distribution
     50%   69.49ms
     75%  155.56ms
     90%  282.09ms
     99%  696.93ms
  745507 requests in 30.10s, 105.28MB read
  Socket errors: connect 0, read 0, write 0, timeout 1
Requests/sec:  24768.69
Transfer/sec:      3.50MB

```

@hydra1983 submitted a pull request for akka-http and here is the result.

@cortwave submitted a pull request to upgrade to version 2.4.11. Here is the latest result.
```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    12.21ms   30.77ms 712.06ms   98.78%
    Req/Sec    33.52k     3.99k   68.36k    86.96%
  Latency Distribution
     50%    8.57ms
     75%   13.30ms
     90%   18.62ms
     99%   52.13ms
  3972310 requests in 30.06s, 587.18MB read
Requests/sec: 132157.96
Transfer/sec:     19.54MB

```

@dpapworth submitted a pull request to add play-java and here is the result.

```
 steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
 Running 30s test @ http://localhost:8080
   4 threads and 128 connections
   Thread Stats   Avg      Stdev     Max   +/- Stdev
     Latency    12.15ms   14.27ms 375.72ms   89.98%
     Req/Sec    44.60k     7.32k   86.18k    73.83%
   Latency Distribution
      50%    8.20ms
      75%   15.65ms
      90%   26.44ms
      99%   60.57ms
   5325273 requests in 30.05s, 655.14MB read
 Requests/sec: 177202.75
 Transfer/sec:     21.80MB
```

Add iris which is a go web framework based on fasthttp and here is the result.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     5.77ms   11.26ms 181.19ms   90.98%
    Req/Sec   208.26k    36.36k  347.64k    74.83%
  Latency Distribution
     50%    2.06ms
     75%    4.54ms
     90%   15.21ms
     99%   57.44ms
  24886288 requests in 30.05s, 3.31GB read
Requests/sec: 828035.66
Transfer/sec:    112.92MB

```

@greenlaw110 submitted a pull request to add actframework and here is the result.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     2.22ms    6.58ms 219.99ms   97.98%
    Req/Sec   241.95k    59.46k  420.20k    73.85%
  Latency Distribution
     50%    1.45ms
     75%    2.24ms
     90%    3.65ms
     99%   11.87ms
  28389984 requests in 30.03s, 3.99GB read
Requests/sec: 945429.13
Transfer/sec:    136.15MB
```

@greenlaw110 submitted a pull request to add JFinal and here is the result.

```
steve@joy:~/tool/wrk$  wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    11.89ms   13.66ms 308.54ms   91.36%
    Req/Sec    35.82k     9.34k   69.40k    70.64%
  Latency Distribution
     50%    8.55ms
     75%   14.81ms
     90%   23.92ms
     99%   59.50ms
  4195471 requests in 30.08s, 0.88GB read
Requests/sec: 139467.87
Transfer/sec:     29.79MB

```

@greenlaw110 submitted a pull request to add NijinFramework and here is the result.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    55.76ms   63.72ms   1.05s    90.55%
    Req/Sec    12.11k     2.93k   24.49k    77.75%
  Latency Distribution
     50%   38.35ms
     75%   71.44ms
     90%  116.40ms
     99%  324.54ms
  1442613 requests in 30.08s, 411.36MB read
Requests/sec:  47956.43
Transfer/sec:     13.67MB
```

@greenlaw110 submitted a pull request to add Play1 and here is the result.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:9000 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:9000
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    10.73ms   23.78ms 397.31ms    0.00%
    Req/Sec    11.32k     2.41k   14.02k    86.33%
  Latency Distribution
     50%    0.00us
     75%    0.00us
     90%    0.00us
     99%    0.00us
  1335580 requests in 30.02s, 562.98MB read
Requests/sec:  44491.87
Transfer/sec:     18.75MB

```


@rygel submitted a pull request to add Pippo-Jetty and here is the result.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    15.66ms   26.96ms 464.86ms   93.37%
    Req/Sec    45.05k    18.29k  100.74k    69.23%
  Latency Distribution
     50%    8.11ms
     75%   16.11ms
     90%   31.43ms
     99%  149.57ms
  5356385 requests in 30.08s, 807.10MB read
Requests/sec: 178055.45
Transfer/sec:     26.83MB

```

@rygel submitted a pull request to add Pippo-Tomcat and here is the result.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    23.50ms   40.19ms 768.53ms   93.01%
    Req/Sec    26.57k    11.43k   86.99k    70.86%
  Latency Distribution
     50%   12.15ms
     75%   24.84ms
     90%   49.50ms
     99%  204.89ms
  3125385 requests in 30.07s, 459.58MB read
Requests/sec: 103948.18
Transfer/sec:     15.29MB

```

@rygel submitted a pull request to add Pippo-Undertow and here is the result.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     9.80ms   21.25ms 448.49ms   95.90%
    Req/Sec    54.74k    16.92k   85.44k    77.53%
  Latency Distribution
     50%    5.44ms
     75%    9.18ms
     90%   15.85ms
     99%  109.31ms
  6500688 requests in 30.06s, 0.92GB read
Requests/sec: 216254.56
Transfer/sec:     31.35MB

```
@gonzalovazquez submitted a pull request to add node-uws and here is the result.  

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     7.22ms   69.98ms   1.64s    99.15%
    Req/Sec   148.28k    28.41k  295.52k    93.92%
  Latency Distribution
     50%    1.88ms
     75%    2.73ms
     90%    3.24ms
     99%    6.91ms
  17706848 requests in 30.02s, 861.21MB read
  Socket errors: connect 0, read 0, write 0, timeout 4
Requests/sec: 589924.44
Transfer/sec:     28.69MB

```

@seanjburns submitted a pull request to add vertx and here is the result.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     2.37ms    3.24ms  79.48ms   90.49%
    Req/Sec   201.91k    19.79k  269.09k    78.08%
  Latency Distribution
     50%    1.41ms
     75%    2.42ms
     90%    5.41ms
     99%   16.08ms
  24114240 requests in 30.02s, 2.87GB read
Requests/sec: 803311.31
Transfer/sec:     98.06MB

```

@kevin-better submitted a pull request to add baseio and here is the result.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    22.20ms   11.17ms 203.34ms   59.61%
    Req/Sec    12.66k     1.85k   15.82k    77.92%
  Latency Distribution
     50%   22.16ms
     75%   32.24ms
     90%   37.42ms
     99%   40.12ms
  1511579 requests in 30.01s, 191.73MB read
Requests/sec:  50361.98
Transfer/sec:      6.39MB

```

@jknack submitted a pull request to upgrade jooby to version 1.1 and here is the result.

```
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     4.31ms    3.32ms  48.26ms   78.72%
    Req/Sec    79.88k     7.98k  152.40k    77.13%
  Latency Distribution
     50%    3.61ms
     75%    5.74ms
     90%    8.06ms
     99%   16.61ms
  9550240 requests in 30.09s, 1.34GB read
Requests/sec: 317385.05
Transfer/sec:     45.70MB

```

@JesHansen submitted a pull request to add dotnet core and here is the result.
 
```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:5000 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:5000
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     2.93ms    2.51ms  45.13ms   85.78%
    Req/Sec   122.23k    10.92k  150.99k    72.25%
  Latency Distribution
     50%    2.35ms
     75%    3.77ms
     90%    5.51ms
     99%   12.84ms
  14599887 requests in 30.03s, 1.67GB read
Requests/sec: 486216.93
Transfer/sec:     57.03MB

```

@adrienlauer submitted a pull request to add seedstack-filter and here is the result.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     4.41ms    3.99ms  68.47ms   88.16%
    Req/Sec    86.43k    10.63k  150.72k    74.27%
  Latency Distribution
     50%    3.44ms
     75%    5.71ms
     90%    8.79ms
     99%   18.81ms
  10336608 requests in 30.10s, 1.51GB read
Requests/sec: 343416.33
Transfer/sec:     51.42MB
```

@adrienlauer submitted a pull request to add seedstack-jersey2 and here is the result.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    26.88ms   20.07ms 230.49ms   74.47%
    Req/Sec    13.12k     3.14k   25.28k    75.38%
  Latency Distribution
     50%   22.35ms
     75%   36.26ms
     90%   53.21ms
     99%   93.83ms
  1574128 requests in 30.09s, 357.29MB read
Requests/sec:  52310.11
Transfer/sec:     11.87MB

```

@jknack submitted a pull request with upgraded Jooby and here is the result. 


```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     3.95ms    3.47ms  74.38ms   87.31%
    Req/Sec    91.09k     9.20k  146.91k    75.65%
  Latency Distribution
     50%    3.18ms
     75%    5.12ms
     90%    7.52ms
     99%   16.20ms
  10896144 requests in 30.10s, 1.41GB read
Requests/sec: 362018.07
Transfer/sec:     47.99MB

```

@rpinaa submitted a pull request to add node-loopback and here is the result.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    34.42ms   22.01ms 535.98ms   68.62%
    Req/Sec     8.10k   578.42    11.03k    79.28%
  Latency Distribution
     50%   40.16ms
     75%   59.88ms
     90%    0.00us
     99%    0.00us
  965939 requests in 30.10s, 346.37MB read
Requests/sec:  32091.95
Transfer/sec:     11.51MB

```

@rodrigomata submitted a pull request to add go-httprouter and here is the result.

```
steve@joy:~/tool/wrk$ wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua --latency -- / 16
Running 30s test @ http://localhost:8080
  4 threads and 128 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    14.12ms   14.25ms 171.89ms   87.11%
    Req/Sec    43.19k     5.18k   61.08k    72.83%
  Latency Distribution
     50%    9.58ms
     75%   18.79ms
     90%   32.19ms
     99%   67.61ms
  5164540 requests in 30.05s, 635.36MB read
Requests/sec: 171852.31
Transfer/sec:     21.14MB

```