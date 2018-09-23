---
title:  Early thoughts on Haskell
author: Jono
---

I'm only a month in, and it hasn't been the type drive oasis I had hoped  --- that said it's not all bad.  


The Bad
---------------------

Unsafe functions in the standard prelude --- `head` [throws an exception](http://hackage.haskell.org/package/base-4.11.1.0/docs/src/GHC.List.html#head) if called with an empty list!

Libraries throwing exceptions if there is IO, rather using the type system to indicate the possibility of errors.

The Good
---------------------

Compile time --- after Scala it is blindingly quick. 
 
[hlint](https://hackage.haskell.org/package/hlint) and [ghc_mod](https://hackage.haskell.org/package/ghc-mod) are wonderful, constantly offering succinct ways to structure ones code. 
 
I'm using [Microsoft's Visual Studio Code](https://code.visualstudio.com/) with the [Haskell Language Server](https://marketplace.visualstudio.com/items?itemName=alanz.vscode-hie-server) which is provides a  wrapper around [<abbr title="Haskell IDE Engine">HIE</abbr>](https://github.com/haskell/haskell-ide-engine) and it's mostly wonderful.  I said mostly as sometimes it just stops. The shutdown / startup is so quick that I haven't looked into why and just restart.


### Cabal is helpful 

```
 $ cabal build
Warning: The package list for 'hackage.haskell.org' is 19 days old.
Run 'cabal update' to get the latest list of available packages.
```

A concise and helpful message with a clear path to resolution.

`cabal gen-bounds`[^1] is wonderful, it will attempt to suggest a set of dependency versions for your project. Which means you can add dependencies to your project and not worry immediately what version is needed. 


Next Steps  
---------------------

I am in a privileged position of knowing wonderfully smart and helpful people who have been able to share their experience with the ecosystem. Their learning can be distilled to:  

- Shim libraries to lift errors out of exceptions and into types. A nice example of this being Ambiata's [shimming](https://github.com/ambiata/snooze/blob/master/src/Snooze/Core.hs) of ` http-client` so as not to throw an exception for a non 200 response,
- Use a custom prelude --- such as [protolude](http://hackage.haskell.org/package/protolude), and  
- Deferring IO as far as possible.  

So with my first application in production I'm off to learn about custom preludes and Freer monads. 



[^1]: [gen-bounds](https://www.haskell.org/cabal/users-guide/developing-packages.html#generating-dependency-version-bounds).

