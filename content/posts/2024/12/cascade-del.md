---
title: "Lessons Learned from a Cascade Deletion Incident"
date: 2024-12-19
author: "Warren"
tags: ["Django", "Database", "Restoration", "Data Integrity", "Best Practices"]
---

### Setting the Scene

One evening, a project manager reached out to inform me that some data appeared to be missing from our system. Upon investigating, I discovered that an unintended cascade deletion had occurred due to the use of `on_delete=models.CASCADE`. This resulted in the deletion of not only the target data but also several related records, which were critical to the system's integrity.

### The Restoration Process

1. **Restore from Backup:** I quickly connected with our Site Reliability Engineer (SRE) to retrieve the most recent data backups. After confirming the integrity of the backups, I restored them to a staging environment.
2. **Delta Sync:** After confirming the backup’s integrity, I performed a delta restoration, syncing the backup with the current database to recover the lost data while preserving recent changes.
3. **Code Fixes:** I updated the models, replacing `models.CASCADE` with safer options like `models.PROTECT` or `models.SET_NULL` to prevent accidental deletions in the future.

### Lessons Learned

- **Be Cautious with** `on_delete`: Understand the cascading impact when cleaning up or modifying attributes that affect related records.
- **Backups Matter:** Regular backups are essential for quick recovery.
- **Test Thoroughly:** Ensure changes are tested with edge cases, especially when they involve data relationships.
- **Better Monitoring:** Implement more granular monitoring and alerting for destructive changes to the database.

---

This experience was a wake-up call to double down on best practices, including database integrity checks, better testing, and comprehensive backups. Mistakes happen, but the goal is to learn from them and improve the system.
