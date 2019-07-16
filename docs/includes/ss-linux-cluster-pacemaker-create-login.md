---
ms.openlocfilehash: d2519b1cc56081f8a35308ac41e11f46a7f97211
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68215618"
---
1. **In tutte le istanze di SQL Server creare un account di accesso server per Pacemaker**. Il codice Transact-SQL seguente crea un account di accesso:

   ```Transact-SQL
   USE [master]
   GO
   CREATE LOGIN [pacemakerLogin] with PASSWORD= N'ComplexP@$$w0rd!'
    
   ALTER SERVER ROLE [sysadmin] ADD MEMBER [pacemakerLogin]
   ```

  Al momento della creazione del gruppo di disponibilità, l'utente di pacemaker richiederà le autorizzazioni ALTER, controllo e VIEW DEFINITION per il gruppo di disponibilità, dopo averlo creato, ma prima che tutti i nodi vengono aggiunti a esso.

1. **In tutte le istanze di SQL Server salvare le credenziali per l'account di accesso di SQL Server**.

   ```bash
   echo 'pacemakerLogin' >> ~/pacemaker-passwd
   echo 'ComplexP@$$w0rd!' >> ~/pacemaker-passwd
   sudo mv ~/pacemaker-passwd /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd
   sudo chmod 400 /var/opt/mssql/secrets/passwd # Only readable by root
   ```
