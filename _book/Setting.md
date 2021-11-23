# Using gitbook-cli

https://github.com/GitbookIO/gitbook-cli

## install

```
$ npm init

# -g オプションを指定しない
$ npm install gitbook-cli
```

## Create a book

npm install で -g オプションを指定しない変わりに、 npx で実行

```
$ npx gitbook init
```

### Preview and serve your book

```
$ npx gitbook serve
```

### Build the static website

```
$ npx gitbook build
```