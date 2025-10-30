# ODS-CI 0500__ide Directory Verification Checklist
## Manual Review Template for Test Duplication Analysis

**Repository:** https://github.com/red-hat-data-services/ods-ci  
**Target Directory:** `ods_ci/tests/Tests/0500__ide/`  
**Date:** October 30, 2025

---

## Step 1: Clone and Navigate

```bash
# Clone the repository
git clone https://github.com/red-hat-data-services/ods-ci.git
cd ods-ci/ods_ci/tests/Tests/0500__ide/

# List all test files
find . -name "*.robot" -type f | sort

# Count total test files
find . -name "*.robot" -type f | wc -l
```

**Results:**
```
[ ] Total .robot files found: _______
[ ] Subdirectories present: _______
```

---

## Step 2: List All Test Files

For each `.robot` file found, document:

| # | File Path | File Name | Approx Line Count |
|---|-----------|-----------|-------------------|
| 1 | | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |
| 5 | | | |
| 6 | | | |
| 7 | | | |
| 8 | | | |
| 9 | | | |
| 10 | | | |

---

## Step 3: For Each Test File - Match Against ODH-Dashboard Tests

Use this template for each ods-ci test file:

---

### Test File: `___________________________.robot`

**Test Cases Found:**
1. Test Case Name: _______________________
2. Test Case Name: _______________________
3. Test Case Name: _______________________

**What This Test Does:**
- [ ] Creates workbench/notebook
- [ ] Starts workbench/notebook
- [ ] Stops workbench/notebook
- [ ] Deletes workbench/notebook
- [ ] Checks status/events
- [ ] Validates environment variables
- [ ] Tests PVC/storage attachment
- [ ] Tests permissions/access control
- [ ] Tests image selection
- [ ] Tests failure scenarios
- [ ] Other: _______________________

**Potential ODH-Dashboard Equivalent:**

| ODH-Dashboard Test File | Test Name | Duplication % |
|-------------------------|-----------|---------------|
| | | % |

**Duplication Assessment:**
- [ ] **COMPLETE DUPLICATE** (85-100%) - Recommend DELETE from ods-ci
- [ ] **PARTIAL DUPLICATE** (50-84%) - Recommend REVIEW
- [ ] **UNIQUE** (0-49%) - Recommend KEEP in ods-ci

**Unique Coverage in ODS-CI (if any):**
- 
- 
- 

**Recommendation:**
- [ ] DELETE - Complete duplicate, no unique value
- [ ] REVIEW - Partial duplicate, needs evaluation
- [ ] KEEP - Unique coverage or backend-specific testing

**Notes:**


---

## Step 4: Match Against Known ODH-Dashboard Tests

Here's the complete inventory of ODH-Dashboard workbench tests to compare against:

### ODH-Dashboard Test Inventory

#### 1. testWorkbenchControlSuite.cy.ts
**Location:** `frontend/src/__tests__/cypress/cypress/tests/e2e/dataScienceProjects/workbenches/`

**Test 1:** "Starting, Stopping, Launching and Deleting a Workbench"
- **Tags:** `@Sanity`, `@SanitySet2`, `@ODS-1818`, `@ODS-1823`, `@ODS-1975`
- **Steps:**
  - Login as admin
  - Navigate to project workbenches tab
  - Create workbench with code-server-notebook
  - Wait for Running status
  - Stop workbench → verify Stopped
  - Restart workbench → verify Running
  - Delete workbench → verify deleted
- **Validations:**
  - Status transitions
  - Description displayed
  - Image name correct

**Test 2:** "Verify that a Workbench can be started and stopped using the Event log controls"
- **Tags:** `@Sanity`, `@SanitySet2`, `@ODS-1818`, `@ODS-1823`, `@ODS-1975`
- **Steps:**
  - Create workbench
  - Click status to open modal
  - Stop via modal footer button
  - Start via modal footer button
- **Validations:**
  - Modal status updates (Starting → Stopped → Running)

**Look for in ods-ci:** Tests that start/stop/delete workbenches via UI

---

#### 2. testWorkbenchStatus.cy.ts
**Location:** `frontend/src/__tests__/cypress/cypress/tests/e2e/dataScienceProjects/workbenches/`

**Test:** "Verify user can access progress and event log"
- **Tags:** `@Sanity`, `@SanitySet2`, `@ODS-1970`
- **Steps:**
  - Create workbench
  - Wait for Running
  - Click on Running status
  - Navigate to Events tab
- **Validations:**
  - Progress tab shows Running status
  - Events contain: 'Created container', 'Started container', 'Successfully pulled image'

**Look for in ods-ci:** Tests that check workbench status or event logs

---

#### 3. testWorkbenchCreation.cy.ts
**Location:** `frontend/src/__tests__/cypress/cypress/tests/e2e/dataScienceProjects/workbenches/`

**Test 1:** "Create Workbench from the launcher page"
- **Tags:** `@Sanity`, `@SanitySet1`, `@ODS-1931`, `@ODS-2218`, `@Bug`
- **Steps:**
  - Create workbench
  - Stop workbench
  - Edit workbench (name + description)
  - Verify updates
- **Validations:**
  - Workbench runs
  - Edited details display

**Test 2:** "Delete PV storage, data connection and workbench"
- **Tags:** `@Sanity`, `@SanitySet1`, `@ODS-1931`, `@ODS-2218`
- **Steps:**
  - Create S3 connection
  - Delete connection
  - Delete cluster storage
- **Validations:**
  - Deletions successful

**Look for in ods-ci:** Tests that create, edit, or configure workbenches

---

#### 4. workbenches.cy.ts
**Location:** `frontend/src/__tests__/cypress/cypress/tests/e2e/dataScienceProjects/workbenches/`

**Test:** "Create workbench and connect existent PersistentVolume"
- **Tags:** `@Smoke`, `@SmokeSet1`, `@ODS-1814`
- **Steps:**
  - Create workbench
  - Attach existing PVC
  - Navigate to cluster storage
- **Validations:**
  - PVC attached
  - Connected resources show workbench name

**Look for in ods-ci:** Tests that attach PVCs/storage to workbenches

---

#### 5. testWorkbenchVariables.cy.ts
**Location:** `frontend/src/__tests__/cypress/cypress/tests/e2e/dataScienceProjects/workbenches/`

**Test 1:** "Set environment variables by uploading YAML"
- **Tags:** `@Sanity`, `@SanitySet3`, `@ODS-1883`, `@ODS-1864`
- **Steps:**
  - Create workbench with Secret (upload YAML)
  - Create workbench with ConfigMap (upload YAML)
  - Validate variables in container
- **Validations:**
  - Variables present via oc exec

**Test 2:** "Inject environment variables using Key/Value"
- **Tags:** `@Sanity`, `@SanitySet3`, `@ODS-1883`, `@ODS-1864`
- **Steps:**
  - Create workbench with Secret (Key/Value)
  - Create workbench with ConfigMap (Key/Value)
  - Validate variables in container
- **Validations:**
  - Variables present via oc exec

**Look for in ods-ci:** Tests that set environment variables or secrets in workbenches

---

#### 6. testWorkbenchNegativeTests.cy.ts
**Location:** `frontend/src/__tests__/cypress/cypress/tests/e2e/dataScienceProjects/workbenches/`

**Test 1:** "UI informs users about workbenches failed to start"
- **Tags:** `@Sanity`, `@SanitySet2`, `@ODS-1973`
- **Steps:**
  - Create workbench with large Hardware Profile (insufficient resources)
  - Wait for Failed status
- **Validations:**
  - Status shows "Failed"
  - Modal displays Failed status

**Test 2:** "Cannot create workbench using special characters or long names"
- **Tags:** `@Sanity`, `@SanitySet2`, `@ODS-1973`
- **Steps:**
  - Attempt invalid resource names
- **Validations:**
  - Submit disabled
  - aria-invalid shown

**Look for in ods-ci:** Tests for workbench failures or invalid inputs

---

#### 7. testWorkbenchImages.cy.ts
**Location:** `frontend/src/__tests__/cypress/cypress/tests/e2e/dataScienceProjects/workbenches/`

**Test:** "Workbench images support N/N-1 image versions"
- **Tags:** `@Sanity`, `@SanitySet3`, `@ODS-2131`
- **Steps:**
  - Navigate to workbench creation
  - Check all available images
- **Validations:**
  - Images with 2+ versions show dropdown

**Look for in ods-ci:** Tests that select different notebook images

---

#### 8. testWorkbenchStorageClasses.cy.ts
**Location:** `frontend/src/__tests__/cypress/cypress/tests/e2e/dataScienceProjects/workbenches/`

**Test:** "Create workbench with RWO storage"
- **Tags:** `@Storage`, `@ODS-1931`
- **Steps:**
  - Create cluster storage with custom SC
  - Create workbench and attach
- **Validations:**
  - ReadWriteOnce access mode
  - Storage attached

**Look for in ods-ci:** Tests that use different storage classes

---

#### 9. testWorkbenchTolerations.cy.ts
**Location:** `frontend/src/__tests__/cypress/cypress/tests/e2e/settings/hardwareProfiles/`

**Test 1:** "Workbench Creation using Hardware Profiles with Tolerations"
- **Tags:** `@Sanity`, `@SanitySet2`, `@HardwareProfiles`
- **Steps:**
  - Create workbench with Hardware Profile
  - Validate pod tolerations
- **Validations:**
  - Tolerations in pod spec

**Test 2:** "Validate pod tolerations for stopped workbench"
- **Steps:**
  - Stop workbench
  - Verify pod stops

**Test 3:** "Pod tolerations persist when workbench restarted"
- **Steps:**
  - Delete Hardware Profile
  - Restart workbench
  - Tolerations still present

**Look for in ods-ci:** Tests that use tolerations or node selectors

---

#### 10. testLaunchStandaloneNotebook.cy.ts
**Location:** `frontend/src/__tests__/cypress/cypress/tests/e2e/dataScienceProjects/`

**Test:** "Launch Jupyter from Project Page"
- **Tags:** `@Smoke`, `@SmokeSet1`, `@ODS-1877`, `@NonConcurrent`
- **Steps:**
  - Click "Launch standalone workbench"
  - Select code-server-notebook
  - Start server
  - Open in new tab
  - Stop server
- **Validations:**
  - Pod ready
  - Event log success
  - Can stop

**Look for in ods-ci:** Tests that launch standalone Jupyter notebooks

---

#### 11. testNotebookAdministration.cy.ts
**Location:** `frontend/src/__tests__/cypress/cypress/tests/e2e/applications/enabled/`

**Test 1:** "Admin User Can Access Notebook Administration"
- **Tags:** `@Smoke`, `@SmokeSet1`, `@NotebookAdministration`
- **Steps:**
  - Login as admin
  - Navigate to notebook controller
  - Click administration tab
- **Validations:**
  - Admin tab visible
  - Manage users alert
  - Stop all servers button

**Test 2:** "Non-Admin User cannot Access Notebook Administration"
- **Tags:** `@Smoke`, `@SmokeSet1`, `@NotebookAdministration`
- **Steps:**
  - Login as non-admin
  - Attempt to access admin tab
- **Validations:**
  - Admin tab not visible
  - Admin controls not accessible

**Look for in ods-ci:** Tests for admin access to notebook administration

---

#### 12. testUnauthorizedUserNotebookSpawnBlocked.cy.ts
**Location:** `frontend/src/__tests__/cypress/cypress/tests/e2e/settings/userManagement/`

**Test:** "Unauthorized User Cannot Spawn Jupyter Notebook"
- **Tags:** `@Destructive`, `@ODS-1680`, `@NonConcurrent`
- **Steps:**
  - Remove user from DS user groups
  - Attempt to access dashboard
  - Attempt to spawn notebook
- **Validations:**
  - Unauthorized error shown
  - Cannot access spawner

**Look for in ods-ci:** Tests for user authorization/permissions

---

## Step 5: Summary Report Template

After reviewing all ods-ci test files, complete this summary:

### Complete Duplicates Found (Recommend DELETE from ods-ci)

| # | ODS-CI Test File | ODS-CI Test Case | ODH-Dashboard Equivalent | Duplication % |
|---|------------------|------------------|--------------------------|---------------|
| 1 | | | | % |
| 2 | | | | % |
| 3 | | | | % |
| 4 | | | | % |
| 5 | | | | % |
| 6 | | | | % |

**Total Complete Duplicates:** _______

---

### Partial Duplicates Found (Recommend REVIEW)

| # | ODS-CI Test File | ODS-CI Test Case | ODH-Dashboard Overlap | Unique Coverage in ODS-CI | Duplication % |
|---|------------------|------------------|-----------------------|---------------------------|---------------|
| 1 | | | | | % |
| 2 | | | | | % |
| 3 | | | | | % |
| 4 | | | | | % |

**Total Partial Duplicates:** _______

---

### Unique Tests in ODS-CI (Recommend KEEP)

| # | ODS-CI Test File | ODS-CI Test Case | Unique Coverage | Why Keep |
|---|------------------|------------------|-----------------|----------|
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |
| 4 | | | | |

**Total Unique Tests:** _______

---

## Step 6: Final Statistics

**Before Cleanup:**
- Total ODS-CI tests in 0500__ide: _______
- Total ODH-Dashboard workbench tests: 20
- Overlap: _______ tests (____%)

**After Recommended Cleanup:**
- Complete duplicates to delete: _______
- Partial duplicates to review: _______
- Unique tests to keep: _______
- **Remaining ODS-CI tests:** _______
- **Reduction:** _______ tests (____%)

**Estimated Impact:**
- Test execution time saved: _______ minutes
- Maintenance reduction: _____%

---

## Step 7: Action Items

Based on your findings:

### Immediate Actions
- [ ] Share findings with QE team
- [ ] Get consensus on deletions
- [ ] Create GitHub issues for tracking

### Deletion Plan
- [ ] Create ods-ci branch for cleanup
- [ ] Delete complete duplicates (Phase 1)
- [ ] Review partial duplicates (Phase 2)
- [ ] Update test documentation
- [ ] Create PR with detailed justification

### Monitoring
- [ ] Run full test suite after deletion
- [ ] Monitor for 2-3 releases
- [ ] Document any coverage gaps
- [ ] Update test ownership documentation

---

## Notes and Observations

Use this space to document any important findings:

**Tests that surprised you:**
- 

**Tests that are hard to categorize:**
- 

**Additional observations:**
- 

**Questions for the team:**
- 

---

**Checklist completed by:** _______________________  
**Date:** _______________________  
**Review status:** [ ] Draft [ ] Under Review [ ] Approved [ ] Implemented

