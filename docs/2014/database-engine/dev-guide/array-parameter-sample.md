---
title: Esempio di parametro di matrice | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
ms.assetid: 5d7034ca-ce88-4a7e-8dd9-82f867479e7f
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: a670b2e4f4a7a276f9e026cb650855c8aa2108a4
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933739"
---
# <a name="array-parameter-sample"></a>Esempio Array Parameter
  Talvolta può risultare utile creare, aggiornare o eliminare un set di righe in un database. Sono disponibili diversi modi per eseguire queste operazioni. Uno di questi consiste nel passare una matrice di informazioni da un client a una stored procedure basata sull'integrazione con CLR nel server mediante un tipo di dati per l'integrazione con CLR definito dall'utente. La natura di tale tipo di dati limita a 8.000 byte le dimensioni dei dati forniti al server. Questa opzione non è pertanto utile in caso di dati complessi o di grandi dimensioni. Se i dati disponibili sono semplici e di piccole dimensioni, questa opzione risulta più efficace rispetto alla chiamata di una stored procedure per ogni riga. Passando una matrice, l'ordine dei dati viene mantenuto per le applicazioni in cui tale ordine è importante. Nell'esempio sono inclusi gli elementi seguenti:  
  
1.  Il tipo di dati definito dall'utente `ContactTypeNames`, che include l'elenco dei nomi dei tipi di contatti desiderati.  
  
2.  La stored procedure `usp_EnsureContactTypeNames` implementata come metodo Microsoft Visual C# o Microsoft Visual Basic, che accetta un'istanza del tipo di dati definito dall'utente `ContactTypeNames` e inserisce nuove righe nella tabella `Person.ContactType` per i nomi di contatti inclusi nell'istanza del tipo di dati definito dall'utente e che non sono già presenti nella tabella.  
  
3.  L'applicazione console `TestArrayParameter`, che crea un'istanza del tipo di dati definito dall'utente `ContactTypeNames` sulla base dei parametri della riga di comando passati e quindi richiama la stored procedure `usp_EnsureContactTypeNames` passando l'istanza del tipo di dati definito dall'utente come parametro.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per creare ed eseguire questo progetto, è necessario installare il software seguente:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express è disponibile gratuitamente nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sito Web [di documentazione ed esempi di](https://www.microsoft.com/download/details.aspx?id=42299)Express  
  
-   Database AdventureWorks, disponibile nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sito Web [per sviluppatori di](https://archive.codeplex.com/?p=SqlServerSamples)  
  
-   .NET Framework SDK 2.0 o versione successiva oppure Microsoft Visual Studio 2005 o versione successiva. .NET Framework SDK è disponibile gratuitamente.  
  
-   È necessario inoltre che siano soddisfatte le condizioni seguenti:  
  
-   Per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usata deve essere abilitata l'integrazione con CLR.  
  
-   Per abilitare l'integrazione con CLR, effettuare le operazioni seguenti:  
  
    #### <a name="enabling-clr-integration"></a>Abilitazione dell'integrazione con CLR  
  
    -   Eseguire i comandi [!INCLUDE[tsql](../../includes/tsql-md.md)] seguenti:  
  
     `sp_configure 'clr enabled', 1`  
  
     `GO`  
  
     `RECONFIGURE`  
  
     `GO`  
  
    > [!NOTE]  
    >  Per abilitare CLR, è necessario disporre dell'autorizzazione `ALTER SETTINGS` a livello di server, che viene assegnata implicitamente ai membri dei ruoli predefiniti del server `sysadmin` e `serveradmin`.  
  
-   Il database AdventureWorks deve essere installato nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in uso.  
  
-   Se non si è un amministratore per l' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza di in uso, è necessario disporre di un amministratore per concedere l'autorizzazione **CreateAssembly** per completare l'installazione.  
  
## <a name="building-the-sample"></a>Compilazione dell'esempio  
  
#### <a name="create-and-run-the-sample-by-using-the-following-instructions"></a>Creare ed eseguire l'esempio tramite le istruzioni seguenti:  
  
1.  Aprire un prompt dei comandi di .NET Framework o Visual Studio.  
  
2.  Se necessario, creare una directory per l'esempio. Per questo esempio verrà utilizzata la directory C:\MySample.  
  
3.  In c:\MySample creare `ContactTypeNames.vb` (per l'esempio Visual Basic) o `ContactTypeNames.cs` (per l'esempio C#) e copiare nel file il codice di esempio appropriato, Visual Basic o C#, riportato di seguito.  
  
4.  Compilare il codice di esempio nell'assembly necessario dal prompt della riga di comando eseguendo una delle istruzioni seguenti, a seconda del linguaggio scelto.  
  
    -   `Vbc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll  /target:library ContactTypeNames.vb`  
  
    -   `Csc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll /target:library ContactTypeNames.cs`  
  
5.  In c:\MySample creare `Program.vb` (per l'esempio Visual Basic) o `Program.cs` (per l'esempio C#) e copiare nel file il codice di esempio appropriato, Visual Basic o C#, riportato di seguito.  
  
6.  Individuare la riga appropriata nel file Program (intorno alla riga 24) e sostituire `XXX` con il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
    -   `Dim connection As New SqlConnection("data source=XXX;initial catalog=AdventureWorks;Integrated Security=SSPI")`  
  
    -   `using (SqlConnection connection = new SqlConnection("data source=XXX;initial catalog=AdventureWorks;Integrated Security=SSPI"))`  
  
7.  Compilare il codice di esempio nell'eseguibile necessario dal prompt della riga di comando eseguendo una delle istruzioni seguenti, a seconda del linguaggio scelto.  
  
    -   `vbc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Deployment.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Drawing.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Windows.Forms.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll,C:\MySample\ContactTypeNames.dll /out:TestArrayParameter Program.vb`  
  
    -   `Csc /reference:ContactTypeNames.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll /out:TestArrayParameter.exe Program.cs`  
  
8.  Copiare il codice di installazione [!INCLUDE[tsql](../../includes/tsql-md.md)] in un file e salvarlo come `Install.sql` nella directory dell'esempio.  
  
9. Se l'esempio è installato in una directory diversa da `C:\MySample\`, modificare il file `Install.sql` come indicato, in modo che punti al percorso appropriato.  
  
10. Distribuire l'assembly, la stored procedure e le funzioni eseguendo  
  
    -   `sqlcmd -E -I -i install.sql`  
  
11. Testare l'applicazione eseguendo la riga seguente al prompt dei comandi:  
  
    -   `TestArrayParameter "Executive Sales Representative" "Executive Sales Manager"`  
  
12. Copiare lo script di pulizia [!INCLUDE[tsql](../../includes/tsql-md.md)] in un file e salvarlo come `cleanup.sql` nella directory dell'esempio.  
  
13. Eseguire lo script con il comando seguente  
  
    -   `sqlcmd -E -I -i cleanup.sql`  
  
## <a name="sample-code"></a>Codice di esempio  
 Di seguito sono illustrati i listati di codice per l'esempio.  
  
 Di seguito è riportato il codice per la libreria `ContactTypeNames.`  
  
 C#  
  
```  
#region Using directives  
  
using System;  
using System.Data;  
using System.Data.Sql;  
using System.Data.SqlTypes;  
using System.Collections;  
using System.Collections.Generic;  
using System.Text;  
using System.Globalization;  
using Microsoft.SqlServer.Server;  
  
#endregion  
  
    // This class is used to demonstrate passing an array of a fairly small number of reasonably small strings  
    // to a CLR integration based stored procedure on the server.  Because a UDT is limited to 8000 bytes  
    // this approach will not work well for large numbers of strings or long strings.  See the contact  
    // creation stored procedure in the AdventureWorks CLR integration sample for an alternative approach  
    // using XML which does not have these limitations.  
    [Serializable]  
    [Microsoft.SqlServer.Server.SqlUserDefinedType(Microsoft.SqlServer.Server.Format.UserDefined, IsByteOrdered = true, MaxByteSize = 8000)]  
    public class ContactTypeNames : INullable, Microsoft.SqlServer.Server.IBinarySerialize  
    {  
  
        #region Constructors  
        private const int maxByteSize = 8000;  
  
        public ContactTypeNames()  
        {  
        }  
  
        public ContactTypeNames(string[] names)  
        {  
            int numberOfCharacters = 0;  
            foreach (string name in names)  
            {  
                if (name.Length == 0)   
                    throw new ArgumentException("Zero length names are not allowed");  
                numberOfCharacters += name.Length;  
            }  
            int dataByteSize = numberOfCharacters*2 //UTF-16 characters take 2 bytes  
                + names.Length*4  //Four byte header for each string  
                + 4                 //Four byte header for null string at end  
                + 1;                //One byte boolean for null flag  
            if (dataByteSize >= maxByteSize)  
                throw new ArgumentException(string.Format(CultureInfo.InvariantCulture, "Data provided occupies {0} bytes but only {1} bytes "  
                    + "are available", dataByteSize, maxByteSize));  
  
            this._names = names;  
        }  
        #endregion  
  
        #region Accessors  
        public string[] GetTypeNameArray()  
        {  
            //Don't let caller modify our copy of the array  
            return (string[])_names.Clone();  
        }  
  
        //This has an odd API because we can only define Transact-SQL functions on static methods.  
        [SqlFunctionAttribute(FillRowMethodName = "FillNameRow")]  
        public static IEnumerable GetContactTypeNames(ContactTypeNames names)  
        {  
            if (names == null)  
                throw new ArgumentNullException("names");  
  
            return names.GetTypeNameArray();  
        }  
  
        public static void FillNameRow(object nameArrayElement, out string contactName)  
        {  
            contactName = (string)nameArrayElement;  
        }  
  
        #endregion  
  
        #region String Conversions  
  
        /// <summary>  
        /// The string format for contact type names is a sequence of names separated by commas  
        /// </summary>  
        /// <param name="s">a string containing contact type names separated by commas</param>  
        /// <returns>An instance of contact type name containing the specified names</returns>  
        [Microsoft.SqlServer.Server.SqlMethod(DataAccess = Microsoft.SqlServer.Server.DataAccessKind.None, IsDeterministic = false, IsMutator = false, IsPrecise = false,  
        SystemDataAccess = Microsoft.SqlServer.Server.SystemDataAccessKind.None)]  
        public static ContactTypeNames Parse(SqlString s)  
        {  
            if (s.IsNull)  
                return Null;  
            return new ContactTypeNames(s.Value.Split(new char[] {','}));  
        }  
  
        /// <summary>  
        /// Convert the contact type names to a string  
        /// </summary>  
        /// <returns>The contact type names separated by commas</returns>  
        public override string ToString()  
        {  
            if (this.IsNull)  
                return null;  
  
            StringBuilder sb = new StringBuilder();  
            foreach (string name in _names)  
            {  
                if (sb.Length > 0) sb.Append(", ");  
                sb.Append(name);  
            }  
  
            return sb.ToString();  
        }  
        #endregion  
  
        #region INullable Members  
  
        public static ContactTypeNames Null  
        {  
            get  
            {  
                return new ContactTypeNames();  
            }  
        }  
        public bool IsNull  
        {  
            get   
            {   
                return _names == null;   
            }  
        }  
  
        #endregion  
  
        #region IBinarySerialize Members  
  
        //Format:   
        //Byte 1: Null flag (boolean) (true = null)  
        //Byte 2 - 7994: Strings with 4 byte length headers,  
        //               last string is a zero length string.  
        //This format is in part dictated by how the BinaryWriter serializes strings.  See  
        //the Microsoft .NET Framework documentation on System.IO.BinaryWriter for more details.  
  
        public void Read(System.IO.BinaryReader r)  
        {  
            if (r.ReadBoolean())  
            {  
                _names = null;  
                return;  
            }  
            List<String> nameList = new List<String>();  
            string name;  
            while ((name = r.ReadString()).Length != 0)  
            {  
                nameList.Add(name);  
            }  
            _names = new string[nameList.Count];  
            nameList.CopyTo(_names);  
        }  
  
        public void Write(System.IO.BinaryWriter w)  
        {  
            if (w == null)  
                throw new ArgumentNullException("w");  
  
            w.Write(this.IsNull);  
            foreach (string name in _names)  
            {  
                w.Write(name);  
            }  
            w.Write(string.Empty);              
        }  
  
        #endregion  
  
        #region Private Implementation  
  
        private string[] _names;  
        #endregion  
    }  
```  
  
 Visual Basic  
  
```  
#Region "Using directives"  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports System.Collections  
Imports System.Collections.Generic  
Imports System.Text  
Imports System.Globalization  
Imports Microsoft.SqlServer.Server  
Imports System.Runtime.InteropServices  
#End Region  
  
' This class is used to demonstrate passing an array of a fairly small number of reasonably small strings  
' to a CLR integration based stored procedure on the server.  Because a UDT is limited to 8000 bytes  
' this approach will not work well for large numbers of strings or long strings.  See the contact  
' creation stored procedure in the AdventureWorks CLR integration sample for an alternative approach  
' using XML which does not have these limitations.  
<Serializable()> _  
<SqlUserDefinedType(Format.UserDefined, IsByteOrdered:=True, maxByteSize:=8000), CLSCompliant(False)> _  
Public Class ContactTypeNames  
    Implements INullable, IBinarySerialize  
  
#Region "Constructors"  
    Private Const maxByteSize As Integer = 8000  
  
    Public Sub New()  
    End Sub  
  
    Public Sub New(ByVal names() As String)  
        Dim numberOfCharacters As Integer = 0  
  
        For Each name As String In names  
            If name.Length = 0 Then  
                Throw New ArgumentException("Zero length names are not allowed")  
            End If  
  
            numberOfCharacters += name.Length  
        Next  
  
        'UTF-16 characters take 2 bytes  
        'Four byte header for each string  
        'Four byte header for null string at end  
        'One byte boolean for null flag  
        Dim dataByteSize As Integer = numberOfCharacters * 2 _  
            + names.Length * 4 _  
            + 4 _  
            + 1  
  
        If dataByteSize >= maxByteSize Then  
            Throw New ArgumentException(String.Format(CultureInfo.InvariantCulture, _  
                "Data provided occupies {0} bytes but only {1} bytes are available", _  
                dataByteSize, maxByteSize))  
        End If  
  
        Me._names = names  
    End Sub  
#End Region  
  
#Region "Accessors"  
  
    Public Function GetTypeNameArray() As String()  
        'Don't let caller modify our copy of the array  
        Return CType(Me._names.Clone(), String())  
    End Function  
  
    'This has an odd API because we can only define Transact-SQL functions on static methods.  
    <SqlFunction(FillRowMethodName:="FillNameRow", TableDefinition:="[Name] [Name]")> _  
    Public Shared Function GetContactTypeNames(ByVal names As ContactTypeNames) As IEnumerable  
        If names Is Nothing Then  
            Throw New ArgumentNullException("names")  
        End If  
  
        Return names.GetTypeNameArray()  
    End Function  
  
    Public Shared Sub FillNameRow(ByVal nameArrayElement As Object, <Out()> ByRef contactName As String)  
        contactName = CStr(nameArrayElement)  
    End Sub  
  
#End Region  
  
#Region "String Conversions"  
  
    ''' <summary>  
    ''' The string format for contact type names is a sequence of names separated by commas  
    ''' </summary>  
    ''' <param name="s">a string containing contact type names separated by commas</param>  
    ''' <returns>An instance of contact type name containing the specified names</returns>  
    <Microsoft.SqlServer.Server.SqlMethod(DataAccess:=Microsoft.SqlServer.Server.DataAccessKind.None, IsDeterministic:=False, IsMutator:=False, IsPrecise:=False, SystemDataAccess:=Microsoft.SqlServer.Server.SystemDataAccessKind.None)> _  
    Public Shared Function Parse(ByVal s As SqlString) As ContactTypeNames  
        If s.IsNull Then  
            Return Nothing  
        End If  
  
        Return New ContactTypeNames(s.Value.Split(New Char() {","c}))  
    End Function  
  
    ''' <summary>  
    ''' Convert the contact type names to a string  
    ''' </summary>  
    ''' <returns>The contact type names separated by commas</returns>  
    Public Overrides Function ToString() As String  
        If Me.IsNull Then  
            Return Nothing  
        End If  
  
        Dim sb As New StringBuilder()  
  
        For Each name As String In Me._names  
            If sb.Length > 0 Then  
                sb.Append(", ")  
            End If  
  
            sb.Append(name)  
        Next name  
  
        Return sb.ToString()  
    End Function  
#End Region  
  
#Region "INullable Members"  
  
    Shared ReadOnly Property Null() As ContactTypeNames  
        Get  
            Return New ContactTypeNames()  
        End Get  
    End Property  
  
    Public ReadOnly Property IsNull() As Boolean Implements INullable.IsNull  
        Get  
            Return Me._names Is Nothing  
        End Get  
    End Property  
  
#End Region  
  
#Region "IBinarySerialize Members"  
  
    'Format:   
    'Byte 1: Null flag (boolean) (true = null)  
    'Byte 2 - 7994: Strings with 4 byte length headers,  
    '               last string is a zero length string.  
    'This format is in part dictated by how the BinaryWriter serializes strings.  See  
    'the Microsoft .NET Framework documentation on System.IO.BinaryWriter for more details.  
    Public Sub Read(ByVal r As System.IO.BinaryReader) Implements IBinarySerialize.Read  
        If r.ReadBoolean() Then  
            Me._names = Nothing  
            Return  
        End If  
  
        Dim nameList As New List(Of String)  
        Dim name As String = r.ReadString()  
        While name.Length <> 0  
            nameList.Add(name)  
            name = r.ReadString()  
        End While  
  
        Me._names = New String(nameList.Count - 1) {}  
        nameList.CopyTo(Me._names)  
    End Sub  
  
    Public Sub Write(ByVal w As System.IO.BinaryWriter) Implements IBinarySerialize.Write  
        If w Is Nothing Then  
            Throw New ArgumentNullException("w")  
        End If  
  
        w.Write(Me.IsNull)  
  
        For Each name As String In Me._names  
            w.Write(name)  
        Next  
  
        w.Write(String.Empty)  
    End Sub  
  
#End Region  
  
#Region "Private Implementation"  
    Private _names() As String  
#End Region  
  
End Class  
```  
  
 Di seguito è riportato il codice per l'eseguibile di test.  
  
 C#  
  
```  
#region Using directives  
  
using System;  
using System.Collections.Generic;  
using System.Text;  
using System.IO;  
using System.Data;  
using System.Data.Sql;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
#endregion  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            if (args.Length == 0)  
            {  
                Console.WriteLine("Usage: TestArrayParameter contactTypeName1 "  
                    + "contactTypeName2 ... contactTypeNamen");  
                return;  
            }  
            using (SqlConnection connection = new SqlConnection("data source=XXX;initial catalog=AdventureWorks;Integrated Security=SSPI"))  
            {  
                connection.Open();  
                ShowTypeNames(connection, "before any inserts");  
  
                SqlCommand command = connection.CreateCommand();  
                command.CommandText = "usp_EnsureContactTypeNames";  
                command.CommandType = CommandType.StoredProcedure;  
                SqlParameter namesParameter = new SqlParameter("@names", SqlDbType.Udt);  
                namesParameter.UdtTypeName = "ContactTypeNames";  
                namesParameter.Value = new ContactTypeNames(args);  
                command.Parameters.Add(namesParameter);  
                command.ExecuteNonQuery();  
  
                ShowTypeNames(connection, "after any inserts");  
  
            }  
  
        }  
  
        private static void ShowTypeNames(SqlConnection connection, string whenRan)  
        {  
            SqlCommand command = connection.CreateCommand();  
            command.CommandText = "SELECT Name FROM Person.ContactType ORDER BY Name";  
            using (SqlDataReader reader = command.ExecuteReader())  
            {  
                Console.BackgroundColor = ConsoleColor.Blue;  
                Console.Write("Contact type names {0}: ", whenRan);  
                Console.ResetColor();  
                bool first = true;  
                while (reader.Read())  
                {  
                    if (!first) Console.Write(", ");  
                    Console.Write(reader[0].ToString());  
                    first = false;  
                }  
                Console.WriteLine("");  
                Console.WriteLine("");  
            }  
  
        }  
    }  
```  
  
 Visual Basic  
  
```  
#Region "Using directives"  
Imports System  
Imports System.Collections.Generic  
Imports System.Text  
Imports System.IO  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports System.Data.SqlClient  
#End Region  
  
Class Program  
  
    Shared Sub Main(ByVal args() As String)  
        If args.Length = 0 Then  
            Console.WriteLine("Usage: TestArrayParameter contactTypeName1 " _  
                + "contactTypeName2 ... contactTypeNamen")  
            Return  
        End If  
  
        Dim connection As New SqlConnection("data source=XXX;initial catalog=AdventureWorks;Integrated Security=SSPI")  
        Try  
            connection.Open()  
            ShowTypeNames(connection, "Before any inserts")  
  
            Dim command As SqlCommand = connection.CreateCommand()  
            command.CommandText = "usp_EnsureContactTypeNames"  
            command.CommandType = CommandType.StoredProcedure  
            Dim namesParameter As New SqlParameter("@names", SqlDbType.Udt)  
            namesParameter.UdtTypeName = "ContactTypeNames"  
            namesParameter.Value = New ContactTypeNames(args)  
            command.Parameters.Add(namesParameter)  
            command.ExecuteNonQuery()  
  
            ShowTypeNames(connection, "After any inserts")  
        Finally  
            connection.Dispose()  
        End Try  
    End Sub  
  
    Private Shared Sub ShowTypeNames(ByVal connection As SqlConnection, ByVal whenRan As String)  
        Dim command As SqlCommand = connection.CreateCommand()  
        command.CommandText = "SELECT [Name] FROM [Person].[ContactType] ORDER BY Name"  
        Dim reader As SqlDataReader = command.ExecuteReader()  
        Try  
            Console.BackgroundColor = ConsoleColor.Blue  
            Console.Write("Contact type names {0}: ", whenRan)  
            Console.ResetColor()  
            Dim first As Boolean = True  
            While reader.Read()  
                If Not first Then  
                    Console.Write(", ")  
                End If  
  
                Console.Write(reader(0).ToString())  
                first = False  
            End While  
  
            Console.WriteLine("")  
            Console.WriteLine("")  
        Finally  
            reader.Dispose()  
        End Try  
  
    End Sub  
End Class  
```  
  
 Di seguito è illustrato lo script di installazione [!INCLUDE[tsql](../../includes/tsql-md.md)] (`Install.sql`) che consente la distribuzione dell'assembly e la creazione della stored procedure e delle funzioni nel database.  
  
```  
USE AdventureWorks  
GO  
  
-- Drop existing sprocs, type, and assemblies if any.  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_EnsureContactTypeNames')  
DROP PROCEDURE usp_EnsureContactTypeNames;  
GO  
  
IF EXISTS (SELECT * FROM sys.objects WHERE [name] = N'GetContactTypeNames' and (type = 'FS' or type = 'FT'))    
DROP FUNCTION [GetContactTypeNames];  
GO  
  
IF EXISTS (SELECT * FROM sys.types WHERE [name] = 'ContactTypeNames')  
DROP TYPE ContactTypeNames;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'ContactTypeNames')  
DROP ASSEMBLY ContactTypeNames;  
GO  
  
-- Add assemblies, type, and sproc  
  
DECLARE @SamplesPath nvarchar(1024)  
-- You may need to modify the value of the this variable if you have installed the sample someplace other than the default location.  
set @SamplesPath= 'C:\MySample\'  
CREATE ASSEMBLY ContactTypeNames   
FROM @SamplesPath + 'ContactTypeNames.dll'  
WITH permission_set = Safe;  
  
CREATE TYPE ContactTypeNames  
EXTERNAL NAME ContactTypeNames.ContactTypeNames;  
GO  
  
CREATE FUNCTION GetContactTypeNames  
(  
@names dbo.ContactTypeNames  
)  
RETURNS TABLE  
(  
[Name] [Name]  
)  
AS EXTERNAL NAME [ContactTypeNames].[ContactTypeNames].[GetContactTypeNames];  
GO  
  
CREATE PROCEDURE usp_EnsureContactTypeNames  
(  
@names dbo.ContactTypeNames  
)  
AS  
SET NOCOUNT ON;  
  
INSERT Person.ContactType ([Name])  
SELECT [Name] FROM GetContactTypeNames(@names) AS PotentialNames  
WHERE [Name] NOT IN (SELECT [Name] FROM Person.ContactType);   
GO  
```  
  
 Il codice [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente consente di rimuovere l'assembly e la stored procedure dal database.  
  
```  
USE AdventureWorks  
GO  
  
DELETE Person.ContactType WHERE ContactTypeID > 20;  
GO  
  
-- Drop existing sprocs, type, and assemblies if any.  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_EnsureContactTypeNames')  
DROP PROCEDURE usp_EnsureContactTypeNames;  
GO  
  
IF EXISTS (SELECT * FROM sys.objects WHERE [name] = N'GetContactTypeNames' and (type = 'FS' or type = 'FT'))    
DROP FUNCTION [GetContactTypeNames];  
GO  
  
IF EXISTS (SELECT * FROM sys.types WHERE [name] = 'ContactTypeNames')  
DROP TYPE ContactTypeNames;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'ContactTypeNames')  
DROP ASSEMBLY ContactTypeNames;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Scenari di utilizzo ed esempi per l'integrazione con CLR &#40;Common Language Runtime&#41;](../../../2014/database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
  
  
