---
title: Configurare SQL Server per l'utilizzo di Soft-NUMA (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- NUMA
- non-uniform memory access
ms.assetid: 1af22188-e08b-4c80-a27e-4ae6ed9ff969
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: c9acd3857115a2f6fc13e74d4129630286a27323
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53356134"
---
# <a name="configure-sql-server-to-use-soft-numa-sql-server"></a>Configurare SQL Server per l'utilizzo di Soft-NUMA (SQL Server)
I processori moderni sono costituiti da multipli a molti core per socket. Ogni socket è solitamente rappresentato come un unico nodo NUMA. Il motore di database di SQL Server suddivide le varie strutture interne e i thread del servizio per nodo NUMA. Con i processori che contiene 10 o più core per socket, l'uso di NUMA (soft-NUMA) per suddividere i nodi NUMA hardware in genere aumenta la scalabilità e prestazioni.   

> [!NOTE]
> L'architettura soft-NUMA consente di aggiungere processori a caldo.
  
## <a name="automatic-soft-numa"></a>Architettura soft-NUMA automatica

A partire da SQL Server 2014 Service Pack 2, ogni volta che il server del motore di database rileva più di 8 processori fisici all'avvio, vengono creati automaticamente nodi soft-NUMA se il flag di traccia 8079 è abilitato come parametro di avvio. Memorie centrali del processore e con hyperthreading non vengono presi in considerazione per il conteggio dei processori fisici. Quando il numero di processori fisici rilevato è superiore a 8 per ogni socket, il servizio motore di database crea nodi soft-NUMA che idealmente contengono 8 core, può essere tuttavia ridotto a 5 o incrementato a 9 processori logici per nodo. La dimensione del nodo hardware può essere limitata da una maschera di affinità di CPU. Il numero di nodi NUMA non supererà mai il numero massimo di nodi NUMA supportati.

Senza il flag di traccia, soft-NUMA è disabilitato per impostazione predefinita. È possibile abilitare soft-NUMA usando il flag di traccia 8079. Per rendere effettiva la modifica del valore di questa impostazione è necessario riavviare il motore di database.

La figura seguente illustra il tipo di informazioni riguardanti soft-NUMA che verrà visualizzato nel log degli errori di SQL Server quando SQL Server rilevi nodi NUMA hardware con più di 8 processori logici e se il flag di traccia 8079 è abilitato.

![Soft-NUMA](./media/soft-numa-sql-server/soft-numa.PNG)

## <a name="manual-soft-numa"></a>Architettura soft-NUMA manuale
  
Per configurare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per usare soft-NUMA manuale, è necessario modificare il Registro di sistema per aggiungere una maschera di affinità di configurazione di nodo. La maschera soft-NUMA può essere dichiarata come voce del Registro di sistema binaria, DWORD (esadecimale o decimale) o QWORD (esadecimale o decimale). Per configurare un numero maggiore rispetto alle prime 32 CPU, utilizzare i valori del Registro di sistema QWORD o BINARY. I valori QWORD non possono essere usati nelle versioni precedenti a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. È necessario riavviare il [!INCLUDE[ssDE](../../includes/ssde-md.md)] per configurare soft-NUMA.  
  
> [!TIP]  
>  Le CPU sono numerate partendo da 0.  
  
 [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
 Si consideri l'esempio seguente. In un computer con otto CPU non è disponibile NUMA hardware. Vengono configurati tre nodi soft-NUMA. L'istanza A del[!INCLUDE[ssDE](../../includes/ssde-md.md)] è configurata per utilizzare le CPU da 0 a 3. Una seconda istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene installata e configurata per utilizzare le CPU da 4 a 7. Questo esempio può essere rappresentato visivamente come segue:  
  
 `CPUs          0  1  2  3  4  5  6  7`  
  
 `Soft-NUMA   <-N0--><-N1-><----N2---->`  
  
 `SQL Server  <instance A ><instance B>`  
  
 Nell'istanza A che presenta un I/O significativo sono disponibili ora due thread di I/O e un thread Lazywriter mentre nell'istanza B in cui vengono eseguite operazioni con utilizzo elevato del processore sono disponibili solo un thread di I/O e un thread Lazywriter. È possibile assegnare alle istanze quantità di memoria diverse ma, a differenza di quanto avviene con hardware NUMA, entrambe le istanze ricevono memoria dallo stesso blocco di memoria del sistema operativo e non è presente affinità tra memoria e processore.  
  
 Il thread Lazywriter è correlato alla vista del sistema operativo SQL dei nodi di memoria NUMA fisici. Pertanto, qualsiasi elemento venga presentato come nodo NUMA fisico da parte dell'hardware corrisponderà al numero di thread Lazywriter creati. Per altre informazioni, vedere [funzionamento: Soft-NUMA, Thread di completamento i/o, thread di lavoro Lazywriter e nodi di memoria](https://blogs.msdn.com/b/psssql/archive/2010/04/02/how-it-works-soft-numa-i-o-completion-thread-lazy-writer-workers-and-memory-nodes.aspx).  
  
> [!NOTE]  
>  Le chiavi del Registro di sistema di **Soft-NUMA** non vengono copiate quando si aggiorna un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="set-the-cpu-affinity-mask"></a>Impostazione della maschera di affinità della CPU  
  
1.  Eseguire l'istruzione seguente nell'istanza A per configurarla per l'utilizzo delle CPU 0, 1, 2 e 3 impostando la maschera di affinità della CPU:  
  
    ```  
    ALTER SERVER CONFIGURATION   
    SET PROCESS AFFINITY CPU=0 TO 3;  
    ```  
  
2.  Eseguire l'istruzione seguente nell'istanza B per configurarla per l'utilizzo delle CPU 4, 5, 6 e 7 impostando la maschera di affinità della CPU:  
  
    ```  
    ALTER SERVER CONFIGURATION   
    SET PROCESS AFFINITY CPU=4 TO 7;  
    ```  
  
### <a name="map-soft-numa-nodes-to-cpus"></a>Mapping dei nodi soft-NUMA alle CPU  
  
-   Utilizzando l'Editor del Registro di sistema (regedit.exe), aggiungere le chiavi del Registro di sistema seguenti per eseguire il mapping del nodo soft-NUMA 0 alle CPU 0 e 1, del nodo soft-NUMA 1 alle CPU 2 e 3 e del nodo soft-NUMA 2 alle CPU 4, 5, 6 e 7.  
  
     Nell'esempio seguente si presuppone di avere un server DL580 G9 con 18 core per socket (in 4 socket) e ciascun socket si trova nel proprio gruppo K. La configurazione soft-NUMA creata dovrebbe essere simile alla seguente: 6 core per nodo, 3 nodi per gruppo, 4 gruppi.  
  
    |Esempio per un server [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] con più gruppi K|Tipo|Nome del valore|Dati del valore|  
    |------------------------------------------------------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|Raggruppa|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|Raggruppa|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|Raggruppa|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node3|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node3|DWORD|Raggruppa|1|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node4|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node4|DWORD|Raggruppa|1|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node5|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node5|DWORD|Raggruppa|1|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node6|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node6|DWORD|Raggruppa|2|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node7|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node7|DWORD|Raggruppa|2|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node8|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node8|DWORD|Raggruppa|2|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node9|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node9|DWORD|Raggruppa|3|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node10|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node10|DWORD|Raggruppa|3|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node11|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node11|DWORD|Raggruppa|3|  
  
     Esempi aggiuntivi:  
  
    |[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|Tipo|Nome del valore|Dati del valore|  
    |---------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|Raggruppa|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|Raggruppa|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|Raggruppa|0|  
  
    > [!TIP]  
    >  Per specificare le CPU da 60 a 63, usare un valore QWORD di F000000000000000 o un valore BINARY di 1111000000000000000000000000000000000000000000000000000000000000.  
  
    |[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|Tipo|Nome del valore|Dati del valore|  
    |---------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node0|DWORD|Raggruppa|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node1|DWORD|Raggruppa|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node2|DWORD|Raggruppa|0|  
  
    |SQL Server 2008 R2|Tipo|Nome del valore|Dati del valore|  
    |------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node0|DWORD|Raggruppa|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node1|DWORD|Raggruppa|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node2|DWORD|Raggruppa|0|  
  
    |SQL Server 2008|Tipo|Nome del valore|Dati del valore|  
    |---------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
  
    |SQL Server 2005|Tipo|Nome del valore|Dati del valore|  
    |---------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\90\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\90\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\90\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire il mapping delle porte TCP/IP ai nodi NUMA &#40;SQL Server&#41;](map-tcp-ip-ports-to-numa-nodes-sql-server.md)   
 [Opzione di configurazione del server affinity mask](affinity-mask-server-configuration-option.md)   
 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)  
  
  
