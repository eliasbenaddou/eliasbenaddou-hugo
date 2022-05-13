---
title: "Scaling Bitcoin with the Lightning Network ⚡"
date: 2022-05-12T20:21:12+01:00
draft: false
slug: ""
tags: ['Blog']
image: "img/lightning_network.png"
summary: "The hottest topic of the Bitcoin 2022 conference in Miami was surely the Lightning Network, but does this second layer scale Bitcoin and how does it work?"
---

<center>{{< figure src="/img/lightning_network.png" width=500 caption="source: https://cvj.ch/en/focus/background/bitcoin-lightning-network-records-record-growth/"  >}}</center>

This week will go down in the cryptocurrency history books as one of the worst as we watched a top 10 cryptocurrency project lose 98% of it's value overnight (yes, we're looking at you LUNA). 
This serves as a reminder of the difference between Bitcoin and most other cryptocurrencies - the former probably being the most scarce digital asset ever and the latter possibly just a project doomed to fail.

## What is the Lightning Network?

The Lightning Network (LN) is a key development within the Bitcoin ecosystem. Created in 2018, it is one of the most promising features of Bitcoin that could allow it to become a common means of payment. Lightning utilises the underlying blockchain as a means to settle transactions in batches on another layer, without counterparty trust. Lightning aims to overcome some of the pain points in Bitcoin:

- **Fees**: Large transactions incur very little fees whereas small transactions are costly 

- **Speed**: Average of 7 transactions are proceesed per second with a total blocksize of 1 megabyte due to Bitcoin's distirbuted nature

- **Energy**: Transacting Bitcoins requires a lot of computing power

<details>
<summary>What's a blockchain anyway? 🤔 </summary>
<br>
The term 'blockchain' encompasses all the constituent parts of a technology like Bitcoin: peer-to-peer networking, consensus mechanisms and the actual blockchain itself, also known as hash-linked data structures. 
<br>
<br>
<center>{{< figure src="/img/blockchain.jpg" width=500 caption="Representation of the blockchain as a chain of linked hashes. <br>Source: https://preferredbynature.org/newsroom/fsc-blockchain-across-board-five-years"  >}}</center>
<br>
<br>
The list of all transactions ever made with Bitcoin live on the blockchain which a copy of sits on every connected computer. The format ensures the latest entry references the previous entry, preventing any single computer from maliciously altering an earlier block as this would require changes in each subsequent block and would not be unanimously verified.
<br>
<br>

</details>

## How does it work?

I find it easier to understand new concepts by creating an easily digestible story, so let's take a look at an example of transactions taking place over the LN:

<body><center><div class="mxgraph" style="max-width:100%;border:1px solid transparent;" data-mxgraph="{&quot;highlight&quot;:&quot;#0000ff&quot;,&quot;nav&quot;:true,&quot;resize&quot;:true,&quot;toolbar&quot;:&quot;zoom layers tags lightbox&quot;,&quot;edit&quot;:&quot;_blank&quot;,&quot;xml&quot;:&quot;&lt;mxfile host=\&quot;app.diagrams.net\&quot; modified=\&quot;2022-05-13T12:15:02.547Z\&quot; agent=\&quot;5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.0 Safari/605.1.15\&quot; etag=\&quot;4twF71cpMV5zN5UfRne5\&quot; version=\&quot;18.0.3\&quot; type=\&quot;device\&quot;&gt;&lt;diagram id=\&quot;C5RBs43oDa-KdzZeNtuy\&quot; name=\&quot;Page-1\&quot;&gt;7Vrbcts2EP0az7QP9vAiSvajpbhpGidxJmnS9iUDkWuSNUgwAGhJ/fouLrzTtmJbdeLqRSQWiwv37J5dgjrwF9n6JSdF8oZFQA88J1of+C8OPM9zZjO8KMnGSFznxDWSmKeRlTWCD+k/UClaaZlGIDqKkjEq06IrDFmeQyg7MsI5W3XVLhntrlqQGAaCDyGhQ+nnNJKJkR57s0b+K6RxUq3sTk9MT0YqZfskIiERW7VE/tmBv+CMSXOXrRdAlfUqu3x+tflMz6+mL397L76S3+evP779dGgm++VbhtSPwCGX9576r+It+ePV1+gTL9Z/Uue1yL58OXTt3NeEltZg9mHlprIgRGhQ22RcJixmOaFnjXTOWZlHoNZxsNXonDNWoNBF4d8g5cZ6ByklQ1EiM2p7L1kubaer2mYPauEeiHdYwOoJVvIQbtHzrSMSHoO8xTyTGmYMEGAZSL7BcRwokel1d3PEOmpc6zVg4I3F4xtg90egmVLc7jxKr/E2ltpSLVELtenXktn+5q4zQtlcxx1lvDfE9wN/5pObx4qC5KPLhYiQPLRznipTxcufAnwSNIETBPZ6/LOey1FbOBQad6XrusV6dMvuEfZepMA54M2K5FJoGsGfZakAIepBOEuFIPqhSpHmMV7nqQxZmptll6XqkgnopxaqwS5rySWAmhTWIaAn13qtSVMpgF4eVTZATI0ZuqZBsbHsQDyCWl/ai7wmrtyb4wUddB5TIoQNPyE5u6q5TmnXxKW6KVkCvWAilSnLURZiRAGCNb8GLlPkzfOeQpZGkY5yQtN4dMSp7ag19RpzEl7F+gkW1sVylje9jEfAez2rJJXwoSA6dleYkGqjbBv5akuwbsXlMHir1BZYWq8Tm2mumiThTawsaSWImfPwcB/lmmG4Vx5vfGXJb/QTBLhQt2VGT0PJbkNzyaRk2Qh4UlF128dYKWmaw6LOy84DkB0n+AFa2wJ9M6p+F1XPnx0FQ2BHcJ0EO8J1sqdxu6ynaPxUg7zJwJB4mBD0L21EoafimabfJcgVQN7mfZI3vLxkJSV5DDzVGSEBrVGrRlAol1czuu00YHKGyhZZiSUobjrOiSzN9FHEQYg9vz8Fv++ACfr87j81wbve3bV2xeQFZyEoyEdt1vKUZY3CO8PXVv5YRG3C+oVz5MzciXccNL87xM53eiweDLFzx7DzdoWd9yzfk+58/zEu+4AXIDv0AtlXNvhOjnv4Tnu4mRc4O6oHXb2NB6C5RST+aGg+Okg1KHUQnhwFW8E0mGoYz4OpjCvuDvGxl+kbs7FzN+9+74Xw5GQLCnX+Uwqd7gthu6yvCmFskEx5Vb4U6vKRk1yQUFVlujDWO2JhWHJl2VxIkku60QjKxBSz5oiiqqDVVsoiwpjXZx+2UCZYJ4fqTiQA0tbYuoJGN9BuJlN18qFGAwmVTFXFZg5Tcl8BFLatDVxs9kXy8yySfe+pi+TqXH6fmm9Jzf60zp8VcCfbVVBbTDWZ9KbadWo+vj0vPNckMFFJ4Ay5HLjl4U1N+0vOSBQS0RxYo7+Abipy1ickioerEw2jkxGdFpaUhVeYFZoDj5AyAf2EoZZ/gy+MXOh410AhBikmkEa3c0CikwG6LpDWbJcYaY91aLJn/idj/jrqn475T/bMfw/mD9xHY/6g/xq+Y+avTuT+b8wfKOp9l+tiXq40f3drf1IUQFRWYE2ZP0LuC60BFcuzQp+XG5puyUfZ34zmEJVh+3WBIdMQjRzFDLSn9R+d1uuQfrrPmsOT03n7403POdAesusVBvn+MQrWKz3R9kCOAdLNG9//6U6XucdOdyqVNsr+zlAenqhemI98KFxUlLPH+j4fQ7zJ3ViPRPQ9sMZm83c2k+WbfwX6Z/8C&lt;/diagram&gt;&lt;/mxfile&gt;&quot;}"></div>
<script type="text/javascript" src="https://viewer.diagrams.net/js/viewer-static.min.js"></script>
</center></body>

### Smart Contracts

The LN scales by using smart contracts to create a network of channels by allocating payments through other open channels. For example, Pierre could buy a croissant through Marie if she already has an open channel with Charles, who has an open channel with the boulangerie. This ensures the network operates in a decentralised fashion and removes the need for trust between the parties involved.

<body><center><div class="mxgraph" style="max-width:100%;border:1px solid transparent;" data-mxgraph="{&quot;highlight&quot;:&quot;#0000ff&quot;,&quot;nav&quot;:true,&quot;resize&quot;:true,&quot;page&quot;:1,&quot;toolbar&quot;:&quot;pages zoom layers tags lightbox&quot;,&quot;edit&quot;:&quot;_blank&quot;,&quot;xml&quot;:&quot;&lt;mxfile host=\&quot;app.diagrams.net\&quot; modified=\&quot;2022-05-13T15:22:55.090Z\&quot; agent=\&quot;5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.0 Safari/605.1.15\&quot; etag=\&quot;JmMcMANTO2weCHeisyBE\&quot; version=\&quot;18.0.3\&quot; type=\&quot;device\&quot; pages=\&quot;2\&quot;&gt;&lt;diagram id=\&quot;C5RBs43oDa-KdzZeNtuy\&quot; name=\&quot;Page-1\&quot;&gt;7VpbV+M2EP41nNM+wPElDvBIspRul92lh+3S9mWPYg+2i2x5JZkk/fUdXXyNCeGSQmleEms0us03881YyZ4/zRZnnBTJRxYB3fOcaLHnv9vzvCPfx08lWBrBsesYQczTyIjcRnCZ/g1WWKmVaQSioygZozItusKQ5TmEsiMjnLN5V+2a0e6qBYlhRXAZEroqvUojmdhjeYeN/GdI46Ra2R0fm56MVMr2JCIhEZu3RP7pnj/ljEnzlC2mQJXtKrtcvV9e0fOb8dkvv4rv5LfJhy+fvu6byX56yJD6CBxy+eip/yw+kd/ff4++8mLxB3U+iOzbt33Xzn1LaGkNZg8rl5UFIUKD2ibjMmExywk9baQTzso8ArWOg61G55yxAoUuCv8CKZfWO0gpGYoSmVHbe81yaTtd1d7wwHbzgpU8hDV61oUl4THINdYYGT114JbzWHOeActA8iUqcKBEprddDyPWUeNarwEDHyweD4DdH4BmTHH/kyi9xcdYaku1RC3Uxt9LZvubp84IZXMdd5Tx3hDfD/xDn9w9VhQkH1wuRMjkvp3zRJkqnv0Q4EnQBE4Q2O+jH/VcjtrCvtC4K13XLRaDW3YPsPciBc4BH+Ykl0LTCH7MSgUIUQfhLBWC6EOVIs1j/J6kMmRpbpadlapLJqBPLVSDXdeSawA1KSxCQE+u9VqTplIAvT6obICYGjN0TYNiY9kV8QBqfWkv8pq4cu+OF3TQSUyJEDb8hOTspuY6pV0Tl+qmZAb0golUpixHWYghBgjW5Ba4TJE3z3sKWRpFOsoJTePBESe2o9bUa0xIeBPrE0yti+Usb3oZj4D3euZJKuGyIDqY55iOHkwFakuwWBu8ttcLLK0vu/lq3iQJb2RlSStBHDpPD/dB8lkN98rjja/M+J1+ggAX6rHM6Eko2To0Z0xKlg2AJxVVt32MlZKmOUzrvOw8AdmnEfwDUPW7qHr+4UGwCuwArqNgS7iOdjRul/UUjZ9o3JcZGBIPE4L+pY0o9FQ80/Q7AzkHyNu8T/KGl2espCSPgac6IySgNWrVCArl8mpGt50GTM5Q2SIrsQTFTcc5kaWZPoo4CLHj9zfK7/5LE7zr3V9rV0xecBaCgnzQZi1PmdUofDZ8beXPRdQmrN85B86hO/KOguZzi9j5To/Fg1Xs3CHsvG1h572F96R7338qD32+FyA79ALZVzb4jo56+I57uJk3OjuqB129jSeguUEkvno0tw1SDUodhMcHwUYwrUy1Gs8rUxnf3B7iQy/Td2Zj537efe2F8Oh4Awp1/lUKHe8KYbusrwphbJBMeVU+E+rrCye5IKGqynRhrHfEwrDkyrK5kCSXdKkRlIkpZs0VRVVBq62URYQxr+8+bKFMsE4O1ZNIAKStsXUFjW6gPU+m6uZDjQYSKpmqis0cpuS+AShsWxu4WO6K5LdZJPveSxfJ1b38LjWvSc3+uM6fFXDHm1VQG0w1GvWm2nZqPlqfF95qEhipJHCKXA7c8vCypv0ZZyQKiWgurNFfQDcVOesbEsXD1Y2G0cmITgszysIbzArNhUdImYB+wlDLf8QXRi50vGugEIMUE0ij27kg0ckAXRdIa7ZrjLTnujTZMf+LMX8d9S/H/Mc75n8E8wfuszF/0H8N3zLzVzdy/zfmDxT1fs51MS/nmr+7tT8pCiAqK7CmzB8g96nWgIrlWaHvyw1Nt+SD7G9Gc4jKsP26wJBBiEaOYgba0fp/ndbrkH65nzVXb04n7R9ves6B55RdrzDI969RsF7piTYHcgiQbt54/bc7XeYeut2pVNoo+1tDefVG9cL8yIfCaUU5O6wf82OIN7of64GIfgTW2Gz+zmayfPOfQP/0Hw==&lt;/diagram&gt;&lt;diagram id=\&quot;yiduLYJVGX7zm0YBDAw6\&quot; name=\&quot;Page-2\&quot;&gt;7VjJUuMwEP2aHJmyLWU7JiEwh6GKKagCjsJubIHidikKSebrR47lRXbWgRCK4ZT0U7eW91pqyS0ymiwuJUuiKwxAtDwnWLTIecvzXMdx9E+KLHOk72VIKHlgsBK44X8gdzTojAcwtRwVolA8sUEf4xh8ZWFMSpzbbk8o7FETFkIDuPGZaKJ3PFBRhva8bon/BB5G+chup5+1TFjubFYyjViA8wpExi0ykogq+zdZjECk7OW8ZHEXG1qLiUmI1V4BtwP6fNnnFwN69yiTs9+3V/LMTPaViZlZsJmsWuYMQKAJMSZKFWGIMRPjEh1KnMUBpMM42ip9fiEmGnQ1+AxKLY26bKZQQ5GaCNP6hLEyjW5q6xXJ5X3a3492bj6Y7lfG+cKylrm14Ore9Jn+fyi70FYZlBp5TLbedJEbeTXQFGfShy1kGu4UkyGoLX5ur5BfbxzACehF6EAJgin+ak+EmQQOC78i9Bq5nqLnmN3W6ZhMM3vN6zl2F9nETFSZKQMp2bLilqQO083jtF17HLdtJZ7+k/WYW5U1ltAqOQ9IVG93opZpmOo/j7iCm4StFJvr08lOOcEeQQyZ/xKuwkYoUOqmGGMoWlEGIGst9VQ10wKpYLE9gZp6mwDSpjafxPA7rxw4BooqZw11NmdIRYzDuXZpg+xrDlJCg3K9aGXzOlUSX6BOGheiBjHBw1ibviYJND5MKeT63B2YhgkPgtXpsk5I+8T5TFp2alrSppadNVqSo2m5xwn/VTYO9U69cXpfl2zarVWXU5Odc/vJ7i7veJ9w2/teKLpvvFC8LevbDSGumOTf1WL3nurV9tSayv+x1aLTkHKIM8HiEL4F3acika5dkdYI6ubXq49RtPv/lCRy6ouzR09RgYrXcmFU3r1bXsv/Xrl2F6T+GwvSfi9P0q0pmZXUd3/hUlr7tFLzp4Ru8z/Si5g0dvYoYlLA9PucPrTwkuM907RZfuPLtC8/lZLxXw==&lt;/diagram&gt;&lt;/mxfile&gt;&quot;}"></div>
<script type="text/javascript" src="https://viewer.diagrams.net/js/viewer-static.min.js"></script>
</center></body>

This requires the intermediates to have a high enough balance but further helps reduce the load on the blockchain. Ultimately, Pierre won't have to trust the intermediaries that his croissant payments go through to reach the boulangerie as the protocol will ensure the funds reach the destination or be returned to him. The reason for this is that a receiving payment is dependent on having already forwarded it, thus making it impossible for Marie to be able to steal Pierre's money. The caveat is that if Marie goes offline, the smart contract mechanism will close the channel and it could be a matter of hours to days for the timelock on the contract to expire and return the money owed to Pierre. 

### Security

The main Bitcoin blockchain operates under proof-of-work, which ensures it's securtiy by the economic incentives to operate the protocol. Similarly, the off-chain transactions that take place on the LN layer in parallel enforce fair play through a cryptographic process. If foul play occurs and a party tries to broadcast an older version of the balance sheet in an attempt to close a channel prematurely, other servers will catch this by monitoring the blockchain. This would result in Marie facing a penalty and forfeiting all her funds in the channel to Pierre and so acts as a disincentive to broadcast invalid data.

Participants of the LN will have to monitor the blockchain via software on a 'watcher' node to detect any broadcasts of obsolete transactions. Although this could be outsourced to trusted services, this reinforces users to run full nodes on the Bitcoin network, which may even allows them to earn money for contributing.

## The Future

The LN has made significant progress with the adoption rate rising steadily as more exchanges onboard it and reduce the fees for their customers. El Salvador was the first country globally to adopt Bitcoin as legal tender in 2021 and Lightning is used widely via mobile apps to transact in Bitcoin using QR codes. 

<center>{{< figure src="/img/ln_trend.png"  caption="Increase in Bitcoin transacting using the Lightning Network since inception. <br> Source: https://cvj.ch/en/focus/background/bitcoin-lightning-network-records-record-growth/"  >}}</center>


This technology has the potential to disrupt the payments industry by providing merchants with a low fee for handling transactions and could expand to other assets such as stablecoins. Stablecoins that are backed by physical assets are becoming an integral part of the digital currency space. The UK recently gave the green light on incorporating stablecoins as a payment method and put forward adjustments to the existing regulatory framework. 

Personally I'm quite excited to see how projects like the Lightning Network will evolve over the next decade and to watch the race between countries eager to be leading the new age of digital currencies.

