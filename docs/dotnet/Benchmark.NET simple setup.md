#dotnet #performance

## Install package

```bash
dotnet add pacakge BenchmarkDotNet
```

## Benchmark

```csharp
using BenchmarkDotNet.Attributes;
using BenchmarkDotNet.Running;

namespace Perf.FastLoop {
    [MemoryDiagnoser]
    public class T {
        private readonly int[] array = new int[1000];
        private readonly int x = 1;

        [Benchmark]
        public void SlowLoop() {
            var a = array;
            for (int i = 0; i < 1000; i++)
                a[i] += i + x;
        }

        [Benchmark]
        public void FastLoop() {
            var a = array;
            for (int i = 0; i < 1000; i++)
                a[i] = a[i] + i + x;
        }
    }
}

BenchmarkRunner.Run<Perf.FastLoop.T>();
```

Run

```bash
dotnet run --configuration Release --framework net5.0
```