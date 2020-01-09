3. In tutti i nodi del cluster aprire le porte del firewall di Pacemaker. Per aprire queste porte con `firewalld`, eseguire il comando seguente:

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > Se il firewall non ha una configurazione a disponibilità elevata predefinita, aprire le porte seguenti per Pacemaker.
   >
   > * TCP: porte 2224, 3121, 21064
   > * UDP: porta 5405

1. Installare i pacchetti Pacemaker in tutti i nodi.

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```

2. Impostare la password per l'utente predefinito creato durante l'installazione dei pacchetti Pacemaker e Corosync. Usare la stessa password in tutti i nodi. 

   ```bash
   sudo passwd hacluster
   ```

3. Per riaggiungere i nodi al cluster dopo il riavvio, abilitare e avviare il servizio `pcsd` e Pacemaker. Eseguire il comando seguente in tutti i nodi.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. Creare il cluster. Per creare il cluster, eseguire il comando seguente:

   ```bash
   sudo pcs cluster auth <node1> <node2> <node3> -u hacluster -p <password for hacluster>
   sudo pcs cluster setup --name <clusterName> <node1> <node2> <node3> 
   sudo pcs cluster start --all
   sudo pcs cluster enable --all
   ```
   
   >[!NOTE]
   >Se in precedenza è stato configurato un cluster negli stessi nodi, è necessario usare l'opzione `--force` quando si esegue `pcs cluster setup`. Questa opzione equivale a eseguire `pcs cluster destroy`. Per abilitare nuovamente pacemaker, eseguire `sudo systemctl enable pacemaker`.

5. Installare l'agente delle risorse SQL Server per SQL Server. Eseguire i comandi seguenti in tutti i nodi. 

   ```bash
   sudo yum install mssql-server-ha
   ```
