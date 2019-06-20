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
ms.openlocfilehash: 23e80a2bf02ee6b97449ea3acff38a3937d37000
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "67046730"
---
# <a name="lesson-2-create-a-policy-on-container-and-generate-a-shared-access-signature-sas-key"></a>Lezione 2. creare i criteri per il contenitore e generare una chiave di firma di accesso condivisa (SAS, Shared Access Signature)
  In questa lezione, verrà illustrato come creare criteri del contenitore BLOB e generare una chiave SAS.  
  
 I criteri di accesso archiviati forniscono un livello di controllo aggiuntivo sulle firme di accesso condivise sul lato server. Una firma di accesso condivisa è un URI che concede diritti di accesso limitati a contenitori, BLOB, code e tabelle. Quando si utilizza questa nuova funzionalità avanzata, è necessario creare i criteri in un contenitore con diritti di lettura, scrittura ed elenco.  
  
 È possibile creare i criteri e una firma di accesso condivisa utilizzando uno dei metodi seguenti:  
  
-   Operazioni API REST di Azure: [Crea contenitore](https://msdn.microsoft.com/library/azure/dd179468.aspx), [Set Container ACL](https://msdn.microsoft.com/library/azure/dd179391.aspx), e [Get Container ACL](https://msdn.microsoft.com/library/azure/dd179469.aspx).  
  
-   [Metodo CloudBlobContainer.GetSharedAccessSignature](https://docs.microsoft.com/dotnet/api/microsoft.azure.storage.blob.cloudblobcontainer.getsharedaccesssignature) in Microsoft Azure SDK.  
  
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
  
  
