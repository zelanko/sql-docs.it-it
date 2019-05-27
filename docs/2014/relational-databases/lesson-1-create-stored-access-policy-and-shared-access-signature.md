---
title: Lezione 2. Creare un criterio sul contenitore e generare una chiave di firma di accesso condiviso (SAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 41674d9d-8132-4bff-be4d-85a861419f3d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ea28d9e214546930c38d600a27e8df6e971a9f17
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66090855"
---
# <a name="lesson-2-create-a-policy-on-container-and-generate-a-shared-access-signature-sas-key"></a>Lezione 2. creare i criteri per il contenitore e generare una chiave di firma di accesso condivisa (SAS, Shared Access Signature)
  In questa lezione, verrà illustrato come creare criteri del contenitore BLOB e generare una chiave SAS.  
  
 I criteri di accesso archiviati forniscono un livello di controllo aggiuntivo sulle firme di accesso condivise sul lato server. Una firma di accesso condivisa è un URI che concede diritti di accesso limitati a contenitori, BLOB, code e tabelle. Quando si utilizza questa nuova funzionalità avanzata, è necessario creare i criteri in un contenitore con diritti di lettura, scrittura ed elenco.  
  
 È possibile creare i criteri e una firma di accesso condivisa utilizzando uno dei metodi seguenti:  
  
-   Operazioni API REST di Azure: [Crea contenitore](https://msdn.microsoft.com/library/azure/dd179468.aspx), [Set Container ACL](https://msdn.microsoft.com/library/azure/dd179391.aspx), e [Get Container ACL](https://msdn.microsoft.com/library/azure/dd179469.aspx).  
  
-   [Metodo CloudBlobContainer.GetSharedAccessSignature](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storageclient.cloudblobcontainer.getsharedaccesssignature.aspx) in Microsoft Azure SDK.  
  
    ```  
  
       string signature = blob.GetSharedAccessSignature(new SharedAccessPolicy()   
        {   
            // Specify the expiration time for the signature.   
            SharedAccessExpiryTime = DateTime.Now.Years(1),   
            // Specify the permissions granted by the signature.    
            Permissions = SharedAccessPermissions.Write | SharedAccessPermissions.Read   
        });  
  
    ```  
  
-   Uno strumento di esplorazione di terze parti di Microsoft Azure, ad esempio [Esplora archivi Microsoft Azure](http://azurestorageexplorer.codeplex.com/).  
  
 **Lezione successiva:**  
  
 [Lezione 3: Creare una credenziale di SQL Server](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)  
  
  
