
![image](https://github.com/user-attachments/assets/52c3ddfd-a8eb-428e-935e-129bf224f930)


<h3>🛠️ Backend / Indexer Role</h3>

<p>
  The backend acts as a bridge coordinator — it verifies Ethereum transactions and triggers minting on Avalanche.
</p>

<ul>
  <li>Receives a call from the frontend after ETH is locked</li>
  <li>Scans Ethereum logs from <code>currentBlock - 1</code> to <code>currentBlock + 1</code></li>
  <li>Finds and verifies the event emitted by the ETH contract</li>
  <li>Generates a unique <code>lockId</code> from the transaction</li>
  <li>Calls Avalanche contract's <code>backend_confirmation()</code> function</li>
  <li>Avalanche contract checks the mapping:
    <pre><code>mapping(bytes32 => mapping(address => mapping(uint256 => uint8)))</code></pre>
  </li>
  <li>If valid, it increases confirmation count</li>
  <li>Once confirmations reach 2, Avalanche contract calls <code>mint()</code> to mint wrapped ETH</li>
</ul>

<h4>🔐 Why It’s Important</h4>

<ul>
  <li>Verifies on-chain logs to prevent fraud or spoofing</li>
  <li>Triggers cross-chain mint securely only when ETH is truly received</li>
  <li>Ensures confirmations are tracked before minting</li>
</ul>

<p>
  This backend flow makes the bridge secure, verifiable, and ensures the wrapped tokens are minted only after a valid ETH deposit.
</p>
