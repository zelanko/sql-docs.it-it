---
ms.openlocfilehash: d2519b1cc56081f8a35308ac41e11f46a7f97211
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "68215618"
---
1. **In tutte le istanze di SQL Server creare un account di accesso server per Pacemaker**. Il codice Transact-SQL seguente crea un account di accesso:

   ```Transact-SQL
   USE [master]
   GO
   CREATE LOGIN [pacemakerLogin] with PASSWORD= N'ComplexP@$$w0rd!'
    
   ALTER SERVER ROLE [sysadmin] ADD MEMBER [pacemakerLogin]
   ```

  Al momento della creazione del gruppo di disponibilità, l'utente Pacemaker richiederà le autorizzazioni ALTER, CONTROL e VIEW DEFINITION per il gruppo di disponibilità, dopo che è stato creato, ma prima che vi vengano aggiunti nodi.

1. **In tutte le istanze di SQL Server salvare le credenziali per l'account di accesso di SQL Server**.

   ```bash
   echo 'pacemakerLogin' >> ~/pacemaker-passwd
   echo 'ComplexP@$$w0rd!' >> ~/pacemaker-passwd
   sudo mv ~/pacemaker-passwd /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd
   sudo chmod 400 /var/opt/mssql/secrets/passwd # Only readable by root
   ```
