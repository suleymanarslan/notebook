# Blockchain

Index of Contents:

* [Building Blockchain in Go](#building-blockchain-in-go)
  * [Block](#block)
  * [Blockchain](#blockchain)

## Building Blockchain in Go
Notes from the [Building Blockchain in Go](https://jeiwan.cc/posts/building-blockchain-in-go-part-1/) tutorial.

### Block

Every block stores the valuable information such as transactions, its version, timestamp, etc.


```go
type Block struct {
	Timestamp     int64
	Data          []byte
	PrevBlockHash []byte
	Hash          []byte
}
```

* `Timestamp`: Current timestamp
* `Data`: Valuable information stored in the block
* `Hash`: Hash of the block
* `PrevBlockHash`: Hash of the previous block

**Hash**

Calculating hashes are computationally difficult so make adding blocks difficult.

In this example, we'll keep things simple and just calculate sha256 hash on the concatenated combination.

```
func (block *Block) SetHash() {
	timestamp := []byte(strconv.FormatInt(b.Timestamp, 10))
	headers := bytes.Join([][]byte{b.PrevBlockHash, b.Data, timestamp}, []byte{})
	hash := sha256.Sum256(headers)
	b.Hash = hash[:]
}
```

### Blockchain

A blockchain is an ordered back-linked list. Blocks are stored in the insertion order,
each block is linked to the previous one.

```go
type Blockchain struct {
	Blocks []*Block
}

func (bc *Blockchain) AddBlock(data string) {
	prevBlock := bc.blocks[len(bc.blocks)-1]
	newBlock := NewBlock(data, prevBlock.Hash)
	bc.blocks = append(bc.blocks, newBlock)
}
```

### Proof-of-work

Requirement of performing hard work to put data makes the blockchain
more secure and consistent. A reward is paid for this hard work,
so people get paid for it (a.k.a mining). This mechanism is called
"proof-of-work" and it relies on hard & slow work, fast & easy proof verification.

#### Hashing

A hash is a unique representation of the data it was calculated on.

* Original data can not be restored from a hash.
* Certain data can have only one hash and the hash is unique.
* Changing even one byte in the input data will result in a completely different hash.

[Hashcash](https://en.wikipedia.org/wiki/Hashcash) -the proof-of-work algorithm Bitcoin uses- works
as explained in following steps;

* Take block headers
* Add counter
* Get combination of data and counter
* Check if the hash meets certain requirements;
  * If it does, done
  * If it doesn't, increase the counter and repeat steps 3 and 4


##### Implementation

`TargetBits` is the block header that stores the difficulty level at which block was mined.
For now, we'll skip implementing a target adjusting algorithm and just define the difficulty
as a global constant;

```
const TargetBits = 24

func NewProofOfWork(block *Block) *ProofOfWork {
	target := big.NewInt(1)
	target.Lsh(target, uint(256-TargetBits))

	pow := &ProofOfWork{block, target}

	return pow
}
```

We initialize `big.Int` with the value of 1 and shift it left by `256 - TargetBits`.
256 is the length of a SHA-256 hash in bits, and we'll convert a hash to big integer
check if it's less than the target.

Hexadecimal representation of the target we defined:

```
0x10000000000000000000000000000000000000000000000000000000000
```

Comparing the hashes of `I like donuts` and `I like donutsca07ca`
gives us more clear idea about how this method works; if a hash is lower
than the boudnery it's valid. Lowering the boundary makes the work more difficult.

```
0fac49161af82ed938add1d8725835cc123a1a87b1b196488360e58d4bfb51e3
0000010000000000000000000000000000000000000000000000000000000000
0000008b0f41ec78bab747864db66bcb9fb89920ee75f43fdaaeb5544f7f76ca
```
