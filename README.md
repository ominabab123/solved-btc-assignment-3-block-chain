Download Link: https://assignmentchef.com/product/solved-btc-assignment-3-block-chain
<br>



In this assignment you will implement a node that’s part of a block-chain-based distributed consensus protocol. Specifically, your code will receive incoming transactions and blocks and maintain an updated block chain.




<strong>Files provided:</strong>

<table width="613">

 <tbody>

  <tr>

   <td width="200"><strong>Block.java </strong></td>

   <td width="413">Stores the block data structure.</td>

  </tr>

  <tr>

   <td width="200"><strong>BlockHandler.java </strong><strong> </strong><strong> </strong><strong>ByteArrayWrapper.java </strong></td>

   <td width="413">Uses ​BlockChain.java​ to process a newly received block, create a new block, or process a newly received transaction. A utility file which creates a wrapper for byte arrays such that it could be used as a key in hash functions. (SeeTransactionPool.java​)</td>

  </tr>

  <tr>

   <td width="200"><strong>Transaction.java </strong></td>

   <td width="413">This is similar to Transaction.java as provided in Assignment 1 except for introducing functionality to create a coinbase transaction. Take a look at ​Block.java​ constructor to see how a coinbase transaction is created.</td>

  </tr>

  <tr>

   <td width="200"><strong>TransactionPool.java </strong></td>

   <td width="413">Implements a pool of transactions, required when creating a new block.</td>

  </tr>

  <tr>

   <td width="200"><strong>UTXO.java </strong></td>

   <td width="413">From Assignment 1.</td>

  </tr>

  <tr>

   <td width="200"><strong>UTXOPool.java </strong></td>

   <td width="413">From Assignment 1.</td>

  </tr>

 </tbody>

</table>










<strong> </strong>

<strong>             </strong>

<strong>Files to be used from Assignment 1:  </strong>

<strong>TxHandler.java</strong>​<strong>:</strong>




<table width="622">

 <tbody>

  <tr>

   <td width="622">public​ ​class​ ​TxHandler​ { ​/** Creates a public ledger whose current UTXOPool (collection of unspent      * transaction outputs) is utxoPool. This should make a defensive copy of      * utxoPool by using the UTXOPool(UTXOPool uPool) constructor.*/​public​ ​TxHandler​(​UTXOPool​ utxoPool); ​/** Returns true if*        (1) all outputs claimed by tx are in the current UTXO pool,*        (2) the signatures on each input of tx are valid,*        (3) no UTXO is claimed multiple times by tx,*        (4) all of tx’s output values are non-negative, and*        (5) the sum of tx’s input values is greater than or equal to the sum of             its output values; and false otherwise.*/​public​ ​boolean​ ​isValidTx​(​Transaction​ tx); ​/** Handles each epoch by receiving an unordered array of proposed*        transactions, checking each transaction for correctness,*        returning a mutually valid array of accepted transactions,      * and updating the current UTXO pool as appropriate.*/​public​ ​Transaction​[] ​handleTxs​(​Transaction​[] possibleTxs); }</td>

  </tr>

 </tbody>

</table>




Create a public function ​getUTXOPool()​ in the ​TxHandler.java​ file you have created for assignment 1 and copy the file to your code for assignment 3.




When grading  your code, we will run it with our reference ​TxHandler.java​. <strong> </strong>

<strong> </strong>

<strong> </strong>

<strong> </strong>

<strong> </strong>

<strong>             </strong>

<strong>File to be modified:</strong>

<strong>BlockChain.java </strong>

<table width="624">

 <tbody>

  <tr>

   <td width="624"><strong>// Block Chain should maintain only limited block nodes to satisfy the functions</strong> <strong>// You should not have all the blocks added to the block chain in memory </strong><strong> </strong><strong>// as it would cause a memory overflow.</strong><strong> </strong><strong>public</strong>​ ​<strong>class</strong>​ ​<strong>BlockChain</strong>​<strong> { </strong><strong>    </strong>​<strong>public</strong>​ ​<strong>static</strong>​ ​<strong>final</strong>​ ​<strong>int</strong>​<strong> CUT_OFF_AGE </strong>​<strong>=</strong>​<strong> 10; </strong><strong> </strong><strong>    </strong>​<strong>/** </strong>*  <strong>create an empty block chain with just a genesis block. Assume {</strong>​<strong>@code</strong>​<strong> genesisBlock} is </strong>*  <strong>a valid block </strong><strong>     */</strong><strong>    </strong>​<strong>public</strong>​ ​<strong>BlockChain</strong>​<strong>(</strong>​<strong>Block</strong>​<strong> genesisBlock) { </strong><strong>        </strong>​<strong>// IMPLEMENT THIS</strong><strong>    } </strong><strong> </strong><strong>    </strong>​<strong>/** Get the maximum height block */</strong><strong>    </strong>​<strong>public</strong>​ ​<strong>Block</strong>​ ​<strong>getMaxHeightBlock</strong>​<strong>() { </strong><strong>        </strong>​<strong>// IMPLEMENT THIS</strong><strong>    } </strong><strong> </strong><strong>    </strong>​<strong>/** Get the UTXOPool for mining a new block on top of max height block */</strong><strong>    </strong>​<strong>public</strong>​ ​<strong>UTXOPool</strong>​ ​<strong>getMaxHeightUTXOPool</strong>​<strong>() { </strong><strong>        </strong>​<strong>// IMPLEMENT THIS</strong><strong>    } </strong><strong> </strong><strong>    </strong>​<strong>/** Get the transaction pool to mine a new block */</strong><strong>    </strong>​<strong>public</strong>​ ​<strong>TransactionPool</strong>​ ​<strong>getTransactionPool</strong>​<strong>() { </strong><strong>        </strong>​<strong>// IMPLEMENT THIS</strong><strong>    } </strong><strong> </strong><strong>    </strong>​<strong>/** </strong>*        <strong>Add {</strong>​<strong>@code</strong>​<strong> block} to the block chain if it is valid. For validity, all transactions      * should be valid and block should be at {</strong>​<strong>@code</strong>​<strong> height &gt; (maxHeight – CUT_OFF_AGE)}. </strong>*        <strong>For example, you can try creating a new block over the genesis block (block height 2)      * if the block chain height is {</strong>​<strong>@code</strong>​<strong> &lt;= CUT_OFF_AGE + 1}. As soon as {</strong>​<strong>@code</strong>​<strong> height &gt;      * CUT_OFF_AGE + 1},  you cannot create a new block at height 2. </strong>*        ​<strong>@return</strong>​<strong> true if block is successfully added </strong><strong>     */</strong><strong>    </strong>​<strong>public</strong>​ ​<strong>boolean</strong>​ ​<strong>addBlock</strong>​<strong>(</strong>​<strong>Block</strong>​<strong> block) { </strong><strong>        </strong>​<strong>// IMPLEMENT THIS</strong><strong>    } </strong><strong> </strong><strong>    </strong>​<strong>/** Add a transaction to the transaction pool */</strong><strong>    </strong>​<strong>public</strong>​ ​<strong>void</strong>​ ​<strong>addTransaction</strong>​<strong>(</strong>​<strong>Transaction</strong>​<strong> tx) { </strong><strong>        </strong>​<strong>// IMPLEMENT THIS</strong><strong>    } </strong><strong>}</strong></td>

  </tr>

 </tbody>

</table>

<strong> </strong>

The BlockChain class is responsible for maintaining a block chain. Since the entire block chain could be huge in size, you should only keep around the most recent blocks. The exact number to store is up to your design, as long as you’re able to implement all the API functions.




Since there can be (multiple) forks, blocks form a tree rather than a list. Your design should take this into account. You have to maintain a UTXO pool corresponding to every block on top of which a new block might be created.




<strong>Assumptions and hints: </strong>

<ul>

 <li>A new genesis block won’t be mined. If you receive a block which claims to be a genesis block</li>

</ul>

(parent is a null hash) in the addBlock(Block b)​ function, you can return ​ false​   .​

<ul>

 <li>If there are multiple blocks at the same height, return the oldest block in getMaxHeightBlock() ​ ​</li>

 <li>Assume for simplicity that a coinbase transaction of a block is available to be spent in the next block mined on top of it. (This is contrary to the actual Bitcoin protocol when there is a “maturity” period of 100 confirmations before it can be spent).</li>

 <li>Maintain only one global Transaction Pool for the block chain and keep adding transactions to it on receiving transactions and remove transactions from it if a new block is received or created. It’s okay if some transactions get dropped during a block chain reorganization, i.e., when a side branch becomes the new longest branch. Specifically, transactions present in the original main branch (and thus removed from the transaction pool) but absent in the side branch might get lost.</li>

 <li>The coinbase value is kept constant at 25 bitcoins whereas in reality it halves roughly every 4 years and is currently 12.5 BTC.</li>

 <li>When checking for validity of a newly received block, just checking if the transactions form a</li>

</ul>

valid set is enough. The set need not be a maximum possible set of transactions. Also, you needn’t do any proof-of-work checks.