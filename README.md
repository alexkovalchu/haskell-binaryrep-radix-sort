## Radix sort of numbers and numerically indexed data types, based on binary representation of primitive types

With msd prefix you have parallel Most significant digit radix sort

With lsd prefix you have Least significant digit radix sort

The flag --enable-tests builds the QuickCheck test-suite at (test/test.hs)

    cabal install --enable-tests

or

    cabal configure --enable-tests
    cabal build
    cabal test
    cabal haddock
    ...

Sorting floats (Float, Double) or records with a floating-point index:

```haskell
    {-# LANGUAGE PackageImports #-}

    import Data.List.RadixSort.Base (msdSortFloats)
    import Data.List.RadixSort.HasIndexFloat (HasIndexFloat(..))
    import Data.List as L
    import "random" System.Random
    import Control.Monad
    import Data.Ord

    data FRec = FRec {fieldF:: Float} deriving (Eq, Show)

    instance HasIndexFloat FRec where
        indexFloat = fieldF

    instance Ord FRec where
        compare = comparing indexFloat

    floatExample = do

        listF1 <- replicateM 10 $ getStdRandom (randomR ((-100)::Float,100))
        let listF2 = L.map FRec listF1

        print listF1

        putStrLn "\n"
        print $ msdSortFloats listF1

        putStrLn "\n"
        print $ msdSortFloats listF2

    main = floatExample
```

Sorting integers (type IntN) or records with an IntN index:

```haskell
    {-# LANGUAGE PackageImports #-}

    import Data.List.RadixSort.Base (msdSortInts)
    import Data.List.RadixSort.HasIndexInt32 (HasIndexInt32(..))
    import Data.List as L
    import "random" System.Random
    import Control.Monad
    import Data.Int
    import Data.Ord

    data IRec = IRec {fieldI:: Int32} deriving (Eq, Show)

    instance HasIndexInt32 IRec where
        indexInt32 = fieldI

    instance Ord IRec where
        compare = comparing indexInt32

    intExample = do

        listI1 <- replicateM 10 $ getStdRandom (randomR ((-100)::Int32,100))
        let listI2 = L.map IRec listI1

        print listI1

        putStrLn "\n"
        print $ msdSortInts listI1

        putStrLn "\n"
        print $ msdSortInts listI2


    main = intExample
```

Sorting naturals (type WordN) or records with a WordN index:

```haskell
    {-# LANGUAGE PackageImports #-}

    import Data.List.RadixSort.Base (msdSortNats)
    import Data.List.RadixSort.HasIndexWord32 (HasIndexWord32(..))
    import Data.List as L
    import "random" System.Random
    import Control.Monad
    import Data.Word
    import Data.Ord

    data WRec = WRec {fieldW:: Word32} deriving (Eq, Show)

    instance HasIndexWord32 WRec where
        indexWord32 = fieldW

    instance Ord WRec where
        compare = comparing indexWord32

    wordExample = do

        listN1 <- replicateM 10 $ getStdRandom (randomR (0::Word32,100))
        let listN2 = L.map WRec listN1

        print listN1
        putStrLn "\n"
        print $ msdSortNats listN1

        putStrLn "\n"
        print $ msdSortNats listN2

    main = wordExample

