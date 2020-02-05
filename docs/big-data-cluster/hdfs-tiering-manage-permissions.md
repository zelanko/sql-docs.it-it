---
title: Autorizzazioni per la suddivisione in livelli HDFS per i cluster Big Data di SQL Server
titleSuffix: Manage HDFS tiering permissions for SQL Server Big Data Clusters
description: Gestire la sicurezza per la suddivisione in livelli HDFS nei cluster Big Data di SQL Server, ad esempio le autorizzazioni per altri sistemi basati su Linux.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 758338618a312d8efe92503581ae82d49d353e51
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "73531967"
---
# <a name="manage-hdfs-permissions-for-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Gestire le autorizzazioni HDFS per i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

HDFS (Hadoop Distributed File System) è un file system simile ai file system basati su Linux che usano POSIX per le autorizzazioni per i file. Oltre al modello di autorizzazioni POSIX tradizionale, HDFS supporta anche gli elenchi di controllo di accesso POSIX. Per altre informazioni, vedere l'[articolo di Apache Hadoop sugli elenchi di controllo di accesso](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_.28Access_Control_Lists.29).

Nelle sezioni seguenti vengono forniti esempi di come usare l'interfaccia della riga di comando `azdata` per gestire le autorizzazioni di file e directory HDFS.

## <a name="prerequisites"></a>Prerequisites

- [Cluster Big Data distribuito](deployment-guidance.md)
- [Strumenti per Big Data](deploy-big-data-tools.md)
  
## <a name="hdfs-shell"></a>Shell HDFS

La funzionalità di shell `hdfs` in `azdata` consente di eseguire i comandi direttamente in una shell per gestire le autorizzazioni HDFS per file e directory. Il meccanismo sottostante usa chiamate WebHdfs per eseguire i comandi

Il comando seguente apre la shell.

```bash
azdata bdc hdfs shell
```

Per accedere alla guida per la shell `hdfs` e comprendere come eseguire i comandi, eseguire il comando seguente quando la shell è attiva.

```bash
[hdfs] ?
```

L'esempio seguente mostra come creare una directory, elencare le directory e modificare le autorizzazioni per una directory, nonché assegnare a un utente di nome `bob` l'accesso in lettura, scrittura ed esecuzione alla directory `sales`.

```bash
[hdfs] mkdir sales
[hdfs] ls
rwxr-xr-x  hdfs bdcadmins        0 Oct 09 18:02 system/
rwxrwxr-x admin bdcadmins        0 Oct 10 16:47 sales/
--xrwxrwxrwx  hdfs bdcadmins        0 Oct 09 18:03 tmp/
rwxrwxrwx  hdfs bdcadmins        0 Oct 09 17:59 user/

[hdfs] acl modify  '/sales/' 'user:bob:rwx'
acl modify: Change completed.
[hdfs] acl status  '/sales/'
{
  `AclStatus`: {
    `entries`: [
      `user:bob:rwx`,
      `group::r-x`
    ],
    `group`: `bdcadmins`,
    `owner`: `admin`,
    `permission`: `775`,
    `stickyBit`: false
  }
}
```

## <a name="create-a-directory-in-hdfs-using-azdata"></a>Creare una directory in HDFS usando `azdata`

Creare una directory denominata `data` nel percorso `/sales`.

```bash
azdata bdc hdfs mkdir --path '/sales/data'
```

## <a name="change-owner-of-a-directory-or-file"></a>Modificare il proprietario di una directory o di un file

Modificare l'utente proprietario della directory `data` in HDFS e impostare *`alice`* come utente proprietario e *`salesgroup`* come gruppo proprietario. Per modificare il proprietario, è necessario essere un proprietario.

```bash
azdata bdc hdfs chown --owner alice --group 'salesgroup' --path '/sales/data'
```

## <a name="change-permissions-of-a-file-or-directory-with-chmod"></a>Modificare le autorizzazioni di un file o di una directory con `chmod`

Usare `chmod` per modificare le autorizzazioni per file e directory (per proprietario, gruppo proprietario e altro). Per altre informazioni, vedere [Modifica delle autorizzazioni in un file system Linux](https://www.lifewire.com/uses-of-command-chmod-2201064). In HDFS il modello è lo stesso. Ad esempio:

```bash
azdata bdc hdfs chmod --permission 750 --path /sales/data
```

```bash
azdata bdc hdfs chmod --permission 775 --path /sales/data/file.txt
```

## <a name="set-sticky-bit-on-directories"></a>Impostare uno sticky bit sulle directory

L'impostazione di uno sticky bit sulle directory consente di evitare l'eliminazione o la rilocazione non intenzionale di file. Lo sticky bit limita l'autorizzazione per l'eliminazione o lo spostamento di un file a un utente con privilegi avanzati, un proprietario della directory o un proprietario del file. Questa impostazione non ha alcun effetto sul file. Nell'esempio seguente viene impostato uno sticky bit sulla directory `users` aggiungendo alle autorizzazioni il prefisso `1`.

```bash
azdata bdc hdfs chmod --path /sales/users --permission 1750
```

## <a name="setting-acls-on-files-and-directories"></a>Impostazione di elenchi di controllo di accesso per file e directory

Per impostare elenchi di controllo di accesso per file e directory in HDFS, usare i comandi `azdata`.

Di seguito vengono impostati elenchi di controllo di accesso su una directory e viene assegnato all'utente di nome *`tom`* l'accesso in lettura, scrittura ed esecuzione alla directory *`data`* . 

> [!NOTE]
> Quando si usa il comando `set`, assicurarsi di fornire la specifica completa dell'elenco di controllo di accesso, incluse le informazioni su utente proprietario, gruppo proprietario e altro.

```bash
azdata bdc hdfs acl set --path '/sales' --aclspec  'user::rw-,user:tom:rwx,group::rw-,other::rw-'
```

## <a name="default-acl-on-directories"></a>Elenco di controllo di accesso predefinito sulle directory

L'elenco di controllo di accesso predefinito consente alle sottodirectory di ereditare le autorizzazioni dalla directory padre. Solo le directory possono avere un elenco di controllo di accesso predefinito. Quando viene creato un nuovo file o una sottodirectory, questo eredita automaticamente l'elenco di controllo di accesso predefinito dell'elemento padre. In questo modo, l'elenco di controllo di accesso predefinito verrà ereditato verso il basso in livelli di directory con una profondità arbitraria man mano che vengono create nuove sottodirectory.

Di seguito è riportato un esempio di come impostare l'elenco di controllo di accesso predefinito usando azdata.

```bash
azdata bdc hdfs acl set --path '/sale' --aclspec  'user::rw-,user:tom:rwx,group::rw-,other::rw-,default:group::rw-,default:user::rw-,default:other::rw-'
```

## <a name="next-steps"></a>Passaggi successivi

- [Informazioni di riferimento su `azdata`](reference-azdata.md)

- [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
