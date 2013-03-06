# Radix sort based on binary representation - how-to

With msd prefix you have parallel (shorter time, higher space) Most significant digit radix sort

With lsd prefix you have (shorter space, higher time) Least significant digit radix sort

Sorting floats (Float, Double):

    {-# LANGUAGE PackageImports #-}

    import Data.List.RadixSort.Base (msdSortFloats)
    import Data.List.RadixSort.HasIndexFloat (HasIndexFloat(..))
    import Data.List as L
    import "random" System.Random
    import Control.Monad

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

Sorting integers (type IntN):

    {-# LANGUAGE PackageImports #-}

    import Data.List.RadixSort.Base (msdSortInts)
    import Data.List.RadixSort.HasIndexInt32 (HasIndexInt32(..))
    import Data.List as L
    import "random" System.Random
    import Control.Monad
    import Data.Int

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

Sorting naturals (type WordN):

    {-# LANGUAGE PackageImports #-}

    import Data.List.RadixSort.Base (msdSortNats)
    import Data.List.RadixSort.HasIndexWord32 (HasIndexWord32(..))
    import Data.List as L
    import "random" System.Random
    import Control.Monad
    import Data.Word

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

