# haskell-best-practices
My collection of Haskell best practices 

## Haskell unit test with Test.Hspec
```
module NarcissisticSpec where
import Narcissistic (narcissistic)
import Test.Hspec
import Test.QuickCheck

spec :: Spec
spec = do
  describe "narcissistic" $ do
    it "should work for some examples" $ do
      narcissistic 7    `shouldBe` True
      narcissistic 12   `shouldBe` False
      narcissistic 370  `shouldBe` True
      narcissistic 371  `shouldBe` True
      narcissistic 1634 `shouldBe` True
    it "should work for random numbers" $ do
      property $ forAll (choose (1, 50000)) $ \x ->
        narcissistic x `shouldBe` solution (x :: Integer)
  where solution n = let d = digits n
                     in (==) n . sum . map (^(length d)) $ d
          where digits n = case n `quotRem` 10 of
                            (0,r) -> [r]
                            (q,r) -> r : digits q
```
