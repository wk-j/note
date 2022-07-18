#actions

## Installation

- [How to prevent caching of my Javascript file? - Stack Overflow](https://stackoverflow.com/questions/7413234/how-to-prevent-caching-of-my-javascript-file)

```
brew install act
```

## List job

```
act -l
```

## Execute job

```
act -j job-name
```


## Skip job

```yaml
- name: Some step
  if: ${{ !env.ACT }}
  run: |
```