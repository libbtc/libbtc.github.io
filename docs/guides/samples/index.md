---
layout: toc
---

<h1>libbtc Samples</h1>

<h2 id="best_practices">Best Practices</h2>

<h3 id="best_practices_init">Initialize the library</h3>

The library needs to keep some global state and initialize its
dependencies. You must therefore initialize the library before working
with it

```C
ecc_start(); //will initialize crypto environment
```

Usually you don't need to call the shutdown function as the operating
system will take care of reclaiming resources, but if your application
uses libgit2 in some areas which are not usually active, you can use

```C
ecc_stop();
```

to ask the library to clean up the global state. The cleanup will be
performed once there have been the same number of calls to
`btc_stop()` as there were for `btc_start()`.


<h3 id="best_practices_freeing">Transactions</h3>

deserialize and serialize transactions.

```c
//char *hex_tx // containing some hex transaction data
btc_tx* tx = btc_tx_new();
btc_tx_deserialize(hex_tx, strlen(hex_tx), tx);

cstring* str = cstr_new_sz(1024);
btc_tx_serialize(str, tx);

```

Copy transaction

```c
btc_tx* tx_copy = btc_tx_new();
btc_tx_copy(tx_copy, tx);

```

Get the signature hash

```c
uint8_t sighash[32];
memset(sighash, 0, 32); //empty the hash
cstring* script = cstr_new_buf(script_data, outlen); //a input script, see script doc
btc_tx_sighash(tx, script, 0, SIGHASH_ALL_, sighash);

//your hash will be stored in `sighash`
```

Adding outputs. Currently the system will detect P2PKS and P2SH output addresses and sets the appropriate script.

```c
//&btc_chain_test is a pointer to the global chain structs (see chain.h)
btc_tx_add_address_out(tx, &btc_chain_test, 876543210, "2NFoJeWNrABZQ3YCWdbX9wGEnRge7kDeGzQ");
```




<h3 id="best_practices_freeing">Freeing</h3>

Anytime libbtc fills in a non-`const` pointer for you, you should be using a `_free` call to release the resource.

```c
btc_tx *tx = NULL;
btc_tx_init(tx);
/* … */
btc_tx_free(tx);
```

