# Liveness and the Interchain Stack

In 2018, the Interchain Stack debuted core technologies that comprise the foundational layer of how the Interchain Ecosystem works today. During the architecture and development of CometBFT, the CosmosSDK and IBC, the concept of safety over liveness was and still is a core design principle. Today, these components do not provide distributed performance guarantees today due to several inherent challenges of the decentralized blockchain space. Notable, these constraints are not unique to the Interchain Stack and are common to most layer one blockchain technologies in use today.

The decentralization goals of the Interchain Stack rely on many different parties to not only perform their own compute, transmission, and storage of chain data, but also all arrive at the same conclusion in order to produce a block. At every step of this process, there are many unknown environmental and runtime factors that make it incredibly challenging to offer guarantees around performance at a protocol level. Some of these factors include compute quality and performance, network latency, storage latency, and consensus latency.

While the Interchain Stack offers a robust framework for building novel and groundbreaking blockchains, it does not provide distributed performance guarantees today. Assuming this incorrectly can lead to unreliable and unsafe applications. When developing using the Interchain Stack, it is crucial to consider the following

- Do not assume constant block throughput or timeliness of events. Applications should be designed to handle variability and potential delays of unknown frequency and duration.
- Do not assume a chain’s past performance will continue to remain at that level in the future.
- Design mechanisms to manage timeouts, delays, and retries, ensuring your implementation remains functional under varying network conditions.
- Consider the potential for resource constraints and optimize the use of compute resources, storage, and bandwidth when implementing.

The Interchain Stack stewards continue to identify new areas where components can operate faster and be more resilient under load to aid chains to produce blocks faster and handle more network load more efficiently.
