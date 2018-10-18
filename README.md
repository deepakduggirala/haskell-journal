### TODO

-   [ ] <https://www.hackerrank.com/domains/fp>
-   [ ] Graham Hutton Programming in Haskell remaining chapters exercises and publish here <https://github.com/deepakduggirala/graham-hutton-haskell-vol2-solutions>
-   [ ] Real World Haskell

## Documentation on [Github](https://github.com/deepakduggirala/haskell-journal)

-   Graham Hutton Programming in Haskell Solutions <https://github.com/deepakduggirala/graham-hutton-haskell-vol2-solutions>
-   Stack setup (docker) <https://github.com/deepakduggirala/stack-ghc-docker>
-   SPOJ Problems <https://github.com/deepakduggirala/Haskell-SPOJ>
-   Setting Up a Development Environment (<https://www.vacationlabs.com/haskell/environment-setup.html>)
-   Install stack on Mac OS `curl -sSL https://get.haskellstack.org/ | sh`

1.  VS code extension
    -   `git clone https://github.com/haskell/haskell-ide-engine --recursive`
    -   `cd haskell-ide-engine`
    -   `make build-all`
    -   Install "Haskell Language Server" plugin in VS code
2.  Create a "first-project"
    -   Make note of the resolver used in stack.yaml file of haskell-ide-engine and use it for creating first-project
    -   `stack new --resolver=<RESOLVER> first-project`
    -   `cd first-project`
    -   `stack setup`
    -   Start ghci with `stack ghci`
3.  Haskell Documentation
    -   Find out the resolver from stack.yaml of the project
    -   Go to the [Stackage homepage](https://www.stackage.org/) and find the listing page for your LTS/resolver
    -   Search for documentation and packages only from this page
    -   to add a dependency to the haskell project
        1.  Identify the package the module belongs to. For example Data.Map.Strict belongs to containers package. This info can be found in URL of stackage documentation page
            <https://www.stackage.org/haddock/nightly-2018-09-28/containers-0.5.11.0/Data-Map-Strict.html>
        2.  Add package name to dependencies section of stack.yaml file.
        3.  Run `stack build`. Delete {project}.cabal and rebuild if changes aren't taking effect.
4.  GHCI

    -   function definitions

        -   `let abs n | n >= 0 = n | otherwise = -n`
        -   Pattern matching functions
            ```haskell
              fact 0 = 1
              fact n = n \* fact (n-1)
            ```
            can be written as `let { fact 0 = 1 ; fact n = n * fact (n-1) }`

    -   Importing modules
        -   `:m` resets the imported modules
        -   Qualified import `import qualified Data.ByteString.Lazy as B`
        -   `:l ConvexHull.hs` to load a file

5.  Some Stack wisdom (<https://lexi-lambda.github.io/blog/2018/02/10/an-opinionated-guide-to-haskell-in-2018/> )

    -   Never run `stack install` to install a dependency, it's just an alias for `stack build --copy-bins`
    -   `stack test` is an alias for `stack build --test`
    -   `stack build --file-watch`, watch files and trigger command. Works on other commands as well eg: `stack test --file-watch`
    -   Access local (offline) documentation. `stack haddock --open containers`. containers is the package name.
    -   Local searchable documentation install hoogle, `stack hoogle -- generate --local`. start a local instance of hoogle `stack hoogle -- server --local --port=8080`.

6.  Haskell Gotchas
    -   Exponentiation
        ```haskell
        (^) :: (Num a, Integral b) => a -> b -> a
        (^^) :: (Fractional a, Integral b) => a -> b -> a
        (**) :: Floating a => a -> a -> a
        ```
    -   Precedence <https://gist.github.com/deepakduggirala/f34e721207c39ce3236d177c9f20f558>       
7.  IO

    -   module <b>`Text.Printf`</b> has c like print formatters
    -   Read numbers one per line
        ```haskell
        -- Input:
        -- 2
        -- 5
        -- 3
        -- 4
        -- Output:
        -- 2
        -- 5
        -- 3
        -- 4
        f = id
        main = do
            inputdata <- getContents
            mapM_ (putStrLn. show). f. map read. lines $ inputdata
        ```
