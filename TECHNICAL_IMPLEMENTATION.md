#### Phase 1: SaaS Audit & Identification
I performed a granular audit of the storage exhaustion event via the Google One Management Console to prioritize data for migration.
* **Observation:** Google Photos (**7.35 GB**) was identified as the primary "hotspot," representing ~50% of the total 15GB quota.
* **Strategic Decision:** Categorized "Device Backup" (**3.61 GB**) as non-essential configuration metadata. Prioritized the archival of "Content Data" (Photos/Videos) for the initial migration phase.
  
> **Evidence:** See [Initial Storage Audit](https://github.com/pbobbitt/Google-Drive-Quota-Photos-Optimization-Lab/blob/main/images/Storage%20Audit%20Before.png) in Visual Documentation.

#### Phase 2: SaaS Export Configuration & Fault Tolerance
To migrate the data while maintaining **Data Integrity** and ensuring a successful transfer over a standard residential internet connection, I configured the Google Takeout parameters as follows:

* **Delivery Method:** "Send download link via email" This decouples the export process from the local machine's uptime, allowing Google's servers to handle the heavy processing asynchronously.
* **File Type:** `.zip` Selected for universal compatibility across Windows, macOS, and Linux environments without requiring proprietary extraction tools.
* **Volume Chunking (2GB):** * **Technical Justification:** By segmenting the 11GB+ of identified data into 2GB volumes, I implemented a **Fault Tolerance** strategy. If a network timeout or packet loss occurs during a 10GB download, the entire file is often corrupted. With 2GB chunks, only the affected segment needs to be re-downloaded, saving bandwidth and time.

>**Data Selection:** Isolated **Google Photos** (the primary storage consumer) while deselecting all other Workspace services to minimize export duration and local storage footprint.

#### Phase 3: Physical Migration & Local Ingestion
With the SaaS export prepared, I initiated the physical transfer of data from Google’s servers to a local, NTFS-formatted external storage device.

* **Download Strategy:** Executed a sequential download of the 2GB volumes to prevent bandwidth saturation and ensure session stability.
* **Infrastructure Check:** Verified local disk space availability (Destination Drive) to accommodate the ~11GB payload before initiating the transfer.

#### Phase 4: Data Archival

To maintain a clean workstation environment and adhere to long-term storage best practices, I migrated the verified assets out of the local "Staging" area.

* **Action:** Executed a cut/paste operation of the 4 validated volumes from the `C:\Users\pbobb\Downloads` directory to the external NTFS-formatted physical drive.
* **Technical Justification:** Separating "Staging" (Downloads) from "Production" (External Archive) prevents accidental deletion and ensures the host machine's primary OS drive remains optimized for performance.

#### Phase 5: Data Purging & Risk Mitigation

With the high-resolution masters verified and secured in the physical production archive, I executed the final phase of the storage recovery plan. This required precise configuration to prevent accidental data loss on endpoint devices.

* **Pre-Deletion Safety Configuration:**
    * **Action:** Disabled "Back up & sync" on the primary mobile endpoint (Android/iOS).
    * **Technical Justification:** **Preventing Bidirectional Synchronization Errors.** In a standard sync environment, deleting an asset from the Cloud (SaaS) triggers a downstream command to delete the corresponding local file on the mobile hardware. Disabling this feature decoupled the cloud quota from the physical device storage, ensuring that cloud-side "Quota Recovery" did not impact the user's local mobile assets.
* **Administrative Purge:**
    * **Method:** Utilized the Google Photos Web UI to perform a bulk "Shift-Click" selection of **~7.27 GB** of identified media.
* **Result:** Successfully recovered **~50%** of total account capacity, returning the environment to a "Healthy" status.

> **Evidence:** See [Post Storage Audit](https://github.com/pbobbitt/Google-Drive-Quota-Photos-Optimization-Lab/blob/main/images/Storage%20Audit%20After.png) in Visual Documentation.

#### Phase 6: Configuration Hardening & Preventative Maintenance
To ensure the long-term sustainability of the recovered storage and defer future SaaS subscription costs, I updated the account's data ingestion policy.

* **Action:** Modified Google Photos upload settings from "Original Quality" to "Storage Saver."
* **Technical Justification:** **Optimization of Cloud Bitrate.** "Original Quality" stores files at their native resolution, which consumes the 15GB quota rapidly. "Storage Saver" utilizes Google's advanced compression algorithms to reduce file size with minimal perceptible quality loss.
* **Impact:** This configuration change significantly reduces the "Storage Velocity" (the rate at which the quota is consumed), ensuring that future backups occupy up to 80% less space than the previous baseline.

#### Phase 7: Infrastructure Redesign & Multi-Account Orchestration
To prevent future "Quota Contention" between Gmail and Media assets, I migrated the cloud-ingestion point to a dedicated, isolated Google identity while maintaining a seamless user experience.

* **Action 1: Service Redirection:** Re-enabled "Back up & sync" on the mobile endpoint and redirected all future uploads to a secondary, dedicated storage account.
* **Action 2: Configuration Hardening:** Updated the new account's ingestion policy to **"Storage Saver"** to maximize the 15GB footprint.
* **Action 3: Cross-Account Access (IAM):** Configured **Partner Sharing** between the new storage account and the user's primary Gmail account.
* **Technical Justification:** **Resource Decoupling with Unified Access.** By isolating the media backup to a secondary account, the primary 15GB quota is permanently protected for high-priority communications. Using Partner Sharing ensures a "Single Pane of Glass" experience the user can view and manage all photos from their primary account without the storage overhead.
* **Result:** Established a scalable, redundant, and user-friendly storage architecture that adheres to the principle of "Separation of Concerns."

  
