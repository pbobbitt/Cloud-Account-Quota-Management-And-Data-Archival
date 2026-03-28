# Project Overview
This project documents the end-to-end process of resolving a critical storage exhaustion event within a Google One account. The primary goal was to recover approximately 50% of the 15GB quota by strategically auditing, exporting, and archiving large media files. The project concludes by implementing a redesigned, multi-account infrastructure to prevent future storage conflicts and ensure long-term stability without incurring subscription costs.

## Milestone 1: SaaS Audit & Identification
**Focus:** Analyzing the Google One storage environment to pinpoint the primary cause of the capacity issue and develop a targeted data migration strategy.

*   **Performed a detailed audit of the storage quota** using the Google One Management Console.
*   **Identified Google Photos as the primary "hotspot,"** consuming 7.35 GB, which accounted for nearly 50% of the total 15GB limit.
*   **Made a strategic decision to prioritize the archival of "Content Data"** (photos and videos) while categorizing the 3.61 GB "Device Backup" as non-essential metadata for the initial recovery phase.

> **Evidence:** See **Initial Storage Audit**
<img src="https://github.com/pbobbitt/Google-Drive-Quota-Photos-Optimization-Lab/blob/main/images/Storage%20Audit%20Before.png" alt="A screenshot of the Google One storage breakdown showing Photos as the largest consumer of space." width="70%">
<BR>

## Milestone 2: SaaS Export Configuration & Fault Tolerance
**Focus:** Configuring a secure and reliable data export that ensures data integrity, even when transferring over a potentially unstable residential internet connection.

*   **Configured the data export using Google Takeout.**
    *   **Delivery Method:** Set to "Send download link via email," which allows Google's servers to handle the intensive processing asynchronously, decoupling it from the local machine's uptime.
    *   **File Type:** Chose `.zip` for its universal compatibility across all major operating systems.
    *   **Volume Chunking (2GB):** Implemented a fault tolerance strategy by splitting the 11GB+ export into smaller 2GB files. This prevents a total download failure if a network error occurs, as only the single affected chunk would need to be re-downloaded.
*   **Isolated the data selection to only include Google Photos,** minimizing the export's size and duration.

> **Evidence:** The successful creation of multiple 2GB `.zip` archive files, ready for download.
<BR>

## Milestone 3: Physical Migration & Local Ingestion
**Focus:** Transferring the prepared data chunks from Google's cloud servers to a local, physical storage device.

*   **Verified that the destination external drive had sufficient free space** to accommodate the entire ~11GB data payload.
*   **Executed a sequential download of the 2GB volumes,** a strategy chosen to avoid saturating the network bandwidth and ensure each file transfer completed successfully without session timeouts.

> **Evidence:** The complete set of downloaded `.zip` volumes present in the local machine's "Downloads" folder.
<BR>

## Milestone 4: Data Archival
**Focus:** Moving the verified data from the temporary local staging area to its permanent, long-term archive location.

*   **Executed a cut-and-paste operation to move all validated `.zip` volumes** from the local `C:\Users\pbobb\Downloads` directory to the external NTFS-formatted physical drive.
*   This action separates the temporary "Staging" area from the "Production" archive, which prevents accidental deletion and keeps the primary operating system drive optimized for performance.

> **Evidence:** The external hard drive now containing the complete, archived photo library.
<BR>

## Milestone 5: Data Purging & Risk Mitigation
**Focus:** Safely removing the archived data from the cloud to recover storage space, while implementing critical safeguards to prevent accidental data loss on synced mobile devices.

*   **Performed a critical pre-deletion safety check.**
    *   **Action:** Disabled the "Back up & sync" feature on the primary mobile device.
    *   **Justification:** This step was crucial to prevent a "bidirectional sync error." Normally, deleting a file from the cloud triggers a command to delete the local copy on a synced device. By disabling this feature, we ensured that cleaning the cloud quota would not accidentally wipe the original photos from the user's phone.
*   **Executed an administrative purge of the cloud data.**
    *   Used the Google Photos web interface to perform a bulk "Shift-Click" selection and delete the ~7.27 GB of media that had already been archived.
*   **Confirmed the successful recovery of ~50% of the total account capacity,** returning the storage environment to a healthy, usable status.

> **Evidence:** See **Post-Migration Storage Audit**
<img src="https://github.com/pbobbitt/Google-Drive-Quota-Photos-Optimization-Lab/blob/main/images/Storage%20Audit%20After.png" alt="A screenshot of the Google One storage breakdown showing a significant reduction in used space after the data purge." width="70%">
<BR>

## Milestone 6: Configuration Hardening & Preventative Maintenance
**Focus:** Implementing a new data policy to ensure the long-term health of the recovered storage and prevent a recurrence of the capacity issue.

*   **Modified the Google Photos upload settings from "Original Quality" to "Storage Saver."**
*   **Technical Justification:** The "Original Quality" setting consumes the 15GB quota rapidly. By switching to "Storage Saver," future uploads will be compressed using Google's algorithms, significantly reducing their file size with minimal perceptible loss in quality.
*   **Impact:** This change dramatically reduces the "storage velocity"—the rate at which new data consumes the quota—thereby extending the life of the free storage tier.

> **Evidence:** The updated settings configuration within the Google Photos account.
<BR>

## Milestone 7: Infrastructure Redesign & Multi-Account Orchestration
**Focus:** Engineering a new, more resilient cloud architecture that isolates high-volume media backups from essential services like Gmail, while maintaining a seamless user experience.

*   **Decoupled media backups from the primary account.**
    *   Re-enabled "Back up & sync" on the mobile device but redirected all future photo and video uploads to a completely separate, secondary Google account. This dedicates the new 15GB quota solely to media.
*   **Hardened the new storage account's configuration** by setting its upload policy to "Storage Saver" from the start.
*   **Ensured a unified user experience by configuring "Partner Sharing."**
    *   This feature allows the new storage account to automatically share all its photos with the user's primary account.
    *   **Result:** The user can still view and manage all their photos from their primary account (a "single pane of glass"), but the storage burden is now handled by the isolated secondary account. This permanently protects the primary account's quota for critical communications.

> **Evidence:** The seamless appearance of new photos (backed up to the secondary account) within the primary account's Google Photos interface.
<BR>

## Troubleshooting Log

| Issue Encountered | Root Cause Analysis | Resolution & Verification |
| :--- | :--- | :--- |
| *No issues were encountered during this project.* | | |
