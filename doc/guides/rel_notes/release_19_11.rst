..  SPDX-License-Identifier: BSD-3-Clause
    Copyright 2019 The DPDK contributors

.. include:: <isonum.txt>

DPDK Release 19.11
==================

.. **Read this first.**

   The text in the sections below explains how to update the release notes.

   Use proper spelling, capitalization and punctuation in all sections.

   Variable and config names should be quoted as fixed width text:
   ``LIKE_THIS``.

   Build the docs and view the output file to ensure the changes are correct::

      make doc-guides-html

      xdg-open build/doc/html/guides/rel_notes/release_19_11.html


New Features
------------

.. This section should contain new features added in this release.
   Sample format:

   * **Add a title in the past tense with a full stop.**

     Add a short 1-2 sentence description in the past tense.
     The description should be enough to allow someone scanning
     the release notes to understand the new feature.

     If the feature adds a lot of sub-features you can use a bullet list
     like this:

     * Added feature foo to do something.
     * Enhanced feature bar to do something else.

     Refer to the previous release notes for examples.

     Suggested order in release notes items:
     * Core libs (EAL, mempool, ring, mbuf, buses)
     * Device abstraction libs and PMDs
       - ethdev (lib, PMDs)
       - cryptodev (lib, PMDs)
       - eventdev (lib, PMDs)
       - etc
     * Other libs
     * Apps, Examples, Tools (if significant)

     This section is a comment. Do not overwrite or remove it.
     Also, make sure to start the actual text at the margin.
     =========================================================

* **FreeBSD now supports `--base-virtaddr` EAL option.**

  FreeBSD version now also supports setting base virtual address for mapping
  pages and resources into its address space.

* **Added Lock-free Stack for aarch64.**

  The lock-free stack implementation is enabled for aarch64 platforms.

* **Added support of dynamic fields and flags in mbuf.**

  This new feature adds the ability to dynamically register some room
  for a field or a flag in the mbuf structure. This is typically used
  for specific offload features, where adding a static field or flag
  in the mbuf is not justified.

* **Updated the enic driver.**

  * Added support for Geneve with options offload.
  * Added flow API implementation based on VIC Flow Manager API.

* **Added Hisilicon hns3 PMD.**

  Added the new ``hns3`` net driver for the inbuilt Hisilicon Network
  Subsystem 3(HNS3) network engine found in the Hisilicon Kunpeng 920 SoC.
  See the :doc:`../nics/hns3` guide for more details on this new driver.

* **Added NXP PFE PMD.**

  Added the new PFE driver for the NXP LS1012A platform. See the
  :doc:`../nics/pfe` NIC driver guide for more details on this new driver.

* **Updated iavf PMD.**

  Enable AVX2 data path for iavf PMD.

* **Updated the Intel e1000 driver.**

  Added support for the ``RTE_ETH_DEV_CLOSE_REMOVE`` flag.

* **Updated the Intel ixgbe driver.**

  Added support for the ``RTE_ETH_DEV_CLOSE_REMOVE`` flag.

* **Updated the Intel i40e driver.**

  Added support for the ``RTE_ETH_DEV_CLOSE_REMOVE`` flag.

* **Updated the Intel fm10k driver.**

  Added support for the ``RTE_ETH_DEV_CLOSE_REMOVE`` flag.

* **Added RX/TX packet burst mode get API.**

  Added two new functions ``rte_eth_rx_burst_mode_get`` and
  ``rte_eth_tx_burst_mode_get`` that allow an application
  to retrieve the mode information about RX/TX packet burst
  such as Scalar or Vector, and Vector technology like AVX2.
  Another new function ``rte_eth_burst_mode_option_name`` is
  provided for burst mode options stringification.

* **Updated the Intel ice driver.**

  Updated the Intel ice driver with new features and improvements, including:

  * Added support for device-specific DDP package loading.
  * Added support for handling Receive Flex Descriptor.
  * Added support for protocol extraction on per Rx queue.
  * Added support for Flow Director filter based on generic filter framework.
  * Added support for the ``RTE_ETH_DEV_CLOSE_REMOVE`` flag.
  * Generic filter enhancement
    - Supported pipeline mode.
    - Supported new packet type like PPPoE for switch filter.
  * Supported input set change and symmetric hash by rte_flow RSS action.
  * Added support for GTP Tx checksum offload.

* **Added cryptodev asymmetric session-less operation.**

  Added session-less option to cryptodev asymmetric structure. It works the same
  way as symmetric crypto, corresponding xform is used directly by the crypto op.

* **Updated the Huawei hinic driver.**

  Updated the Huawei hinic driver with new features and improvements, including:

  * Enabled SR-IOV - Partially supported at this point, VFIO only.
  * Supported VLAN filter and VLAN offload.
  * Supported Unicast MAC filter and Multicast MAC filter.
  * Supported Flow director for LACP, VRRP, BGP and so on.
  * Supported FW version get.

* **Updated Mellanox mlx5 driver.**

  Updated Mellanox mlx5 driver with new features and improvements, including:

  * Added support for VLAN pop flow offload command.
  * Added support for VLAN push flow offload command.
  * Added support for VLAN set PCP offload command.
  * Added support for VLAN set VID offload command.
  * Added support for matching on packets withe Geneve tunnel header.

* **Updated the AF_XDP PMD.**

  Updated the AF_XDP PMD. The new features include:

  * Enabled zero copy between application mempools and UMEM by enabling the
    XDP_UMEM_UNALIGNED_CHUNKS UMEM flag.

* **Added Marvell NITROX symmetric crypto PMD.**

  Added a symmetric crypto PMD for Marvell NITROX V security processor.
  See the :doc:`../cryptodevs/nitrox` guide for more details on this new

* **Added asymmetric support to Marvell OCTEON TX crypto PMD.**

  Added support for asymmetric operations in Marvell OCTEON TX cypto PMD.
  Supports RSA and modexp operations.

* **Added Marvell OCTEON TX2 crypto PMD**

  Added a new PMD driver for h/w crypto offload block on ``OCTEON TX2`` SoC.

  See :doc:`../cryptodevs/octeontx2` for more details

* **Updated NXP crypto PMDs for PDCP support.**

  PDCP support is added to DPAA_SEC and DPAA2_SEC PMDs using rte_security APIs.
  Support is added for all sequence number sizes for control and user plane.
  Test application is updated for unit testing.

* **Enabled Single Pass GCM acceleration on QAT GEN3.**

  Added support for Single Pass GCM, available on QAT GEN3 only (Intel
  QuickAssist Technology C4xxx). It is automatically chosen instead of the
  classic 2-pass mode when running on QAT GEN3, significantly improving
  the performance of AES GCM operations.

* **Updated the Intel QuickAssist Technology (QAT) asymmetric crypto PMD.**

  * Added support for asymmetric session-less operations.
  * Added support for RSA algorithm with pair (n, d) private key representation.
  * Added support for RSA algorithm with quintuple private key representation.

* **Updated the Intel QuickAssist Technology (QAT) compression PMD.**

  Added stateful decompression support in the Intel QuickAssist Technology PMD.
  Please note that stateful compression is not supported.

* **Added external buffers support for dpdk-test-compress-perf tool.**

  Added a command line option to dpdk-test-compress-perf tool to allocate
  and use memory zones as external buffers instead of keeping the data directly
  in mbuf areas.

* **Updated the IPSec library.**

  Added SA Database API to ``librte_ipsec``. A new test-sad application is also
  introduced to evaluate and perform custom functional and performance tests
  for IPsec SAD implementation.

* **Introduced FIFO for NTB PMD.**

  Introduced FIFO for NTB (Non-transparent Bridge) PMD to support
  packet based processing.

* **Added eBPF JIT support for arm64.**

  Added eBPF JIT support for arm64 architecture to improve the eBPF program
  performance.

* **Updated testpmd.**

  * Added a console command to testpmd app, ``show port (port_id) ptypes`` which
    gives ability to print port supported ptypes in different protocol layers.


Removed Items
-------------

.. This section should contain removed items in this release. Sample format:

   * Add a short 1-2 sentence description of the removed item
     in the past tense.

   This section is a comment. Do not overwrite or remove it.
   Also, make sure to start the actual text at the margin.
   =========================================================

* Removed duplicated set of commands for Rx offload configuration from testpmd::

    port config all crc-strip|scatter|rx-cksum|rx-timestamp|
                    hw-vlan|hw-vlan-filter|hw-vlan-strip|hw-vlan-extend on|off

  The testpmd commands set that can be used instead
  in order to enable or disable Rx offloading on all Rx queues of a port is::

    port config <port_id> rx_offload crc_strip|scatter|
                                     ipv4_cksum|udp_cksum|tcp_cksum|timestamp|
                                     vlan_strip|vlan_filter|vlan_extend on|off

* Removed AF_XDP pmd_zero copy vdev argument. Support is now auto-detected.

* The following sample applications have been removed in this release:

  * Exception Path
  * L3 Forwarding in a Virtualization Environment
  * Load Balancer
  * Netmap Compatibility
  * Quota and Watermark
  * vhost-scsi


API Changes
-----------

.. This section should contain API changes. Sample format:

   * sample: Add a short 1-2 sentence description of the API change
     which was announced in the previous releases and made in this release.
     Start with a scope label like "ethdev:".
     Use fixed width quotes for ``function_names`` or ``struct_names``.
     Use the past tense.

   This section is a comment. Do not overwrite or remove it.
   Also, make sure to start the actual text at the margin.
   =========================================================

* eal: made the ``lcore_config`` struct and global symbol private.

* eal: removed the ``rte_cpu_check_supported`` function, replaced by
  ``rte_cpu_is_supported`` since dpdk v17.08.

* eal: removed the ``rte_malloc_virt2phy`` function, replaced by
  ``rte_malloc_virt2iova`` since v17.11.

* eal: made the ``rte_config`` struct and ``rte_eal_get_configuration``
  function private.

* mem: hid the internal ``malloc_heap`` structure and the
  ``rte_malloc_heap.h`` header.

* pci: removed the following functions deprecated since dpdk v17.11:

  - ``eal_parse_pci_BDF`` replaced by ``rte_pci_addr_parse``
  - ``eal_parse_pci_DomBDF`` replaced by ``rte_pci_addr_parse``
  - ``rte_eal_compare_pci_addr`` replaced by ``rte_pci_addr_cmp``

* The network structure ``esp_tail`` has been prefixed by ``rte_``.

* The network definitions of PPPoE ethertypes have been prefixed by ``RTE_``.

* The network structure for MPLS has been prefixed by ``rte_``.

* ethdev: changed ``rte_eth_dev_infos_get`` return value from ``void`` to
  ``int`` to provide a way to report various error conditions.

* ethdev: changed ``rte_eth_promiscuous_enable`` and
  ``rte_eth_promiscuous_disable`` return value from ``void`` to ``int`` to
  provide a way to report various error conditions.

* ethdev: changed ``rte_eth_allmulticast_enable`` and
  ``rte_eth_allmulticast_disable`` return value from ``void`` to ``int`` to
  provide a way to report various error conditions.

* ethdev: changed ``rte_eth_dev_xstats_reset`` return value from ``void`` to
  ``int`` to provide a way to report various error conditions.

* ethdev: changed ``rte_eth_link_get`` and ``rte_eth_link_get_nowait``
  return value from ``void`` to ``int`` to provide a way to report various
  error conditions.

* ethdev: changed ``rte_eth_macaddr_get`` return value from ``void`` to
  ``int`` to provide a way to report various error conditions.

* ethdev: changed ``rte_eth_dev_owner_delete`` return value from ``void`` to
  ``int`` to provide a way to report various error conditions.

* event: The function ``rte_event_eth_tx_adapter_enqueue`` takes an additional
  input as ``flags``. Flag ``RTE_EVENT_ETH_TX_ADAPTER_ENQUEUE_SAME_DEST`` which
  has been introduced in this release is used when used when all the packets
  enqueued in the tx adapter are destined for the same Ethernet port & Tx queue.

* sched: The pipe nodes configuration parameters such as number of pipes,
  pipe queue sizes, pipe profiles, etc., are moved from port level structure
  to subport level. This allows different subports of the same port to
  have different configuration for the pipe nodes.


ABI Changes
-----------

.. This section should contain ABI changes. Sample format:

   * sample: Add a short 1-2 sentence description of the ABI change
     which was announced in the previous releases and made in this release.
     Start with a scope label like "ethdev:".
     Use fixed width quotes for ``function_names`` or ``struct_names``.
     Use the past tense.

   This section is a comment. Do not overwrite or remove it.
   Also, make sure to start the actual text at the margin.
   =========================================================

* net: The Ethernet address and other header definitions have changed
  attributes. They have been modified to be aligned on 2-byte boundaries.
  These changes should not impact normal usage because drivers naturally
  align the Ethernet header on receive and all known encapsulations
  preserve the alignment of the header.


Shared Library Versions
-----------------------

.. Update any library version updated in this release
   and prepend with a ``+`` sign, like this:

     libfoo.so.1
   + libupdated.so.2
     libbar.so.1

   This section is a comment. Do not overwrite or remove it.
   =========================================================

The libraries prepended with a plus sign were incremented in this version.

.. code-block:: diff

     librte_acl.so.2
     librte_bbdev.so.1
     librte_bitratestats.so.2
     librte_bpf.so.1
     librte_bus_dpaa.so.2
     librte_bus_fslmc.so.2
     librte_bus_ifpga.so.2
     librte_bus_pci.so.2
     librte_bus_vdev.so.2
     librte_bus_vmbus.so.2
     librte_cfgfile.so.2
     librte_cmdline.so.2
     librte_compressdev.so.1
     librte_cryptodev.so.8
     librte_distributor.so.1
   + librte_eal.so.12
     librte_efd.so.1
   + librte_ethdev.so.13
   + librte_eventdev.so.8
     librte_flow_classify.so.1
     librte_gro.so.1
     librte_gso.so.1
     librte_hash.so.2
     librte_ip_frag.so.1
     librte_ipsec.so.1
     librte_jobstats.so.1
     librte_kni.so.2
     librte_kvargs.so.1
     librte_latencystats.so.1
     librte_lpm.so.2
     librte_mbuf.so.5
     librte_member.so.1
     librte_mempool.so.5
     librte_meter.so.3
     librte_metrics.so.1
     librte_net.so.1
   + librte_pci.so.2
     librte_pdump.so.3
     librte_pipeline.so.3
     librte_pmd_bnxt.so.2
     librte_pmd_bond.so.2
     librte_pmd_i40e.so.2
     librte_pmd_ixgbe.so.2
     librte_pmd_dpaa2_qdma.so.1
     librte_pmd_ring.so.2
     librte_pmd_softnic.so.1
     librte_pmd_vhost.so.2
     librte_port.so.3
     librte_power.so.1
     librte_rawdev.so.1
     librte_rcu.so.1
     librte_reorder.so.1
     librte_ring.so.2
   + librte_sched.so.4
     librte_security.so.2
     librte_stack.so.1
     librte_table.so.3
     librte_timer.so.1
     librte_vhost.so.4


Known Issues
------------

.. This section should contain new known issues in this release. Sample format:

   * **Add title in present tense with full stop.**

     Add a short 1-2 sentence description of the known issue
     in the present tense. Add information on any known workarounds.

   This section is a comment. Do not overwrite or remove it.
   Also, make sure to start the actual text at the margin.
   =========================================================


Tested Platforms
----------------

.. This section should contain a list of platforms that were tested
   with this release.

   The format is:

   * <vendor> platform with <vendor> <type of devices> combinations

     * List of CPU
     * List of OS
     * List of devices
     * Other relevant details...

   This section is a comment. Do not overwrite or remove it.
   Also, make sure to start the actual text at the margin.
   =========================================================

