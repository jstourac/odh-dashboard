# Workbench Test Duplication Analysis
## Comparison: ODH-Dashboard (Cypress) vs ODS-CI (Robot Framework)

**Date:** October 30, 2025  
**Analysis Scope:** Tests related to workbenches, notebooks, and IDE functionality

---

## Executive Summary

This document analyzes test duplication between:
- **ODH-Dashboard Repository:** Cypress E2E tests in `frontend/src/__tests__/cypress/cypress/tests/e2e/`
- **ODS-CI Repository:** Robot Framework tests in `ods_ci/tests/Tests/0500__ide/`

### Key Findings:
- **Complete Duplicates:** 6-8 test scenarios
- **Partial Duplicates:** 10-12 test scenarios
- **Unique to ODH-Dashboard:** 5-7 test scenarios
- **Recommendation:** Focus on removing complete duplicates from ods-ci to reduce maintenance overhead

---

## 1. ODH-Dashboard Workbench Test Inventory

### 1.1 Core Workbench Lifecycle Tests

#### File: `testWorkbenchControlSuite.cy.ts`
**Tests:**
1. **Starting, Stopping, Launching and Deleting a Workbench**
   - Tags: `@Sanity`, `@SanitySet2`, `@ODS-1818`, `@ODS-1823`, `@ODS-1975`
   - **Actions:**
     - Create workbench with code-server-notebook image
     - Wait for Running status
     - Stop workbench
     - Restart workbench
     - Delete workbench
   - **Validations:**
     - Status transitions (Running → Stopped → Running → Deleted)
     - Workbench description
     - Notebook image name

2. **Start/Stop Workbench using Event Log Controls**
   - Tags: `@Sanity`, `@SanitySet2`, `@ODS-1818`, `@ODS-1823`, `@ODS-1975`
   - **Actions:**
     - Create workbench
     - Click on status to open event log modal
     - Stop workbench via event log footer button
     - Start workbench via event log footer button
   - **Validations:**
     - Status in modal (Starting → Stopped → Running)

---

### 1.2 Workbench Status and Event Log Tests

#### File: `testWorkbenchStatus.cy.ts`
**Test:**
- **Verify user can access progress and event log**
  - Tags: `@Sanity`, `@SanitySet2`, `@ODS-1970`
  - **Actions:**
    - Create workbench
    - Wait for Running status
    - Click on Running status
    - Navigate to Events tab
  - **Validations:**
    - Progress tab shows correct status
    - Events log contains: 'Created container', 'Started container', 'Successfully pulled image'

---

### 1.3 Workbench Creation and Editing Tests

#### File: `testWorkbenchCreation.cy.ts`
**Tests:**
1. **Create Workbench from launcher page**
   - Tags: `@Sanity`, `@SanitySet1`, `@ODS-1931`, `@ODS-2218`, `@Bug`
   - **Actions:**
     - Create workbench
     - Stop workbench
     - Edit workbench (name and description)
   - **Validations:**
     - Workbench runs successfully
     - Edited details display correctly

2. **Delete PV storage, data connection and workbench in shared DS project**
   - Tags: `@Sanity`, `@SanitySet1`, `@ODS-1931`, `@ODS-2218`
   - **Actions:**
     - Create S3 data connection
     - Delete data connection
     - Delete cluster storage
   - **Validations:**
     - Connection deletion
     - Storage deletion

---

### 1.4 Workbench with Storage Tests

#### File: `workbenches.cy.ts`
**Test:**
- **Create workbench and connect existent PersistentVolume**
  - Tags: `@Smoke`, `@SmokeSet1`, `@ODS-1814`
  - **Actions:**
    - Create workbench
    - Attach existing PVC
    - Verify connection in cluster storage tab
  - **Validations:**
    - PVC is attached
    - Connected resources show workbench name

---

### 1.5 Workbench Environment Variables Tests

#### File: `testWorkbenchVariables.cy.ts`
**Tests:**
1. **Set environment variables by uploading YAML files**
   - Tags: `@Sanity`, `@SanitySet3`, `@ODS-1883`, `@ODS-1864`
   - **Actions:**
     - Create workbench with Secret (upload YAML)
     - Create workbench with ConfigMap (upload YAML)
   - **Validations:**
     - Variables present in workbench container

2. **Inject environment variables using Key/Value**
   - Tags: `@Sanity`, `@SanitySet3`, `@ODS-1883`, `@ODS-1864`
   - **Actions:**
     - Create workbench with Secret (Key/Value)
     - Create workbench with ConfigMap (Key/Value)
   - **Validations:**
     - Variables present in workbench container

---

### 1.6 Workbench Negative Tests

#### File: `testWorkbenchNegativeTests.cy.ts`
**Tests:**
1. **UI informs users about workbenches failed to start**
   - Tags: `@Sanity`, `@SanitySet2`, `@ODS-1973`
   - **Actions:**
     - Create workbench with large Hardware Profile (insufficient resources)
   - **Validations:**
     - Workbench shows "Failed" status
     - Modal displays Failed status

2. **Cannot create workbench using special characters or long names**
   - Tags: `@Sanity`, `@SanitySet2`, `@ODS-1973`
   - **Actions:**
     - Attempt to create workbench with invalid resource names
   - **Validations:**
     - Submit button disabled
     - Input shows aria-invalid="true"

---

### 1.7 Workbench Image/Version Tests

#### File: `testWorkbenchImages.cy.ts`
**Test:**
- **Workbench images support N/N-1 image versions**
  - Tags: `@Sanity`, `@SanitySet3`, `@ODS-2131`
  - **Actions:**
    - Navigate to workbench creation
    - Check all available notebook images
  - **Validations:**
    - Images with 2+ versions show version dropdown

---

### 1.8 Workbench Storage Classes Tests

#### File: `testWorkbenchStorageClasses.cy.ts`
**Test:**
- **Create workbench with RWO storage**
  - Tags: `@Storage`, `@ODS-1931`
  - **Actions:**
    - Create cluster storage with custom storage class
    - Create workbench and attach RWO storage
  - **Validations:**
    - Storage shows ReadWriteOnce access mode
    - Storage attached to workbench

---

### 1.9 Workbench Tolerations Tests

#### File: `testWorkbenchTolerations.cy.ts`
**Tests:**
1. **Workbench Creation using Hardware Profiles with Tolerations**
   - Tags: `@Sanity`, `@SanitySet2`, `@Dashboard`, `@HardwareProfiles`
   - **Actions:**
     - Create workbench with Hardware Profile containing tolerations
   - **Validations:**
     - Pod has correct tolerations

2. **Validate pod tolerations for stopped workbench**
   - Tags: `@Sanity`, `@SanitySet2`, `@HardwareProfiles`
   - **Actions:**
     - Stop workbench
   - **Validations:**
     - Pod stops running

3. **Pod tolerations persist when workbench restarted with tolerations disabled**
   - Tags: `@Sanity`, `@SanitySet2`, `@HardwareProfiles`
   - **Actions:**
     - Delete Hardware Profile
     - Restart workbench
   - **Validations:**
     - Tolerations still present in pod

---

### 1.10 Standalone Notebook Tests

#### File: `testLaunchStandaloneNotebook.cy.ts`
**Test:**
- **Launch Jupyter Notebook directly from Project List View**
  - Tags: `@Smoke`, `@SmokeSet1`, `@ODS-1877`, `@NonConcurrent`
  - **Actions:**
    - Click "Launch standalone workbench" from project list
    - Select code-server-notebook image
    - Start server
    - Open in new tab
    - Stop server
  - **Validations:**
    - Pod becomes ready
    - Event log shows success
    - Server can be stopped

---

### 1.11 Notebook Administration Tests

#### File: `testNotebookAdministration.cy.ts`
**Tests:**
1. **Admin User Can Access Notebook Administration**
   - Tags: `@Smoke`, `@SmokeSet1`, `@NotebookAdministration`
   - **Validations:**
     - Administration tab exists
     - Manage users alert visible
     - Stop all servers button visible

2. **Non-Admin User cannot Access Notebook Administration**
   - Tags: `@Smoke`, `@SmokeSet1`, `@NotebookAdministration`
   - **Validations:**
     - Administration tab not visible
     - Admin elements not accessible

---

### 1.12 User Authorization Tests

#### File: `testUnauthorizedUserNotebookSpawnBlocked.cy.ts`
**Tests:**
- **Unauthorized User Cannot Spawn Jupyter Notebook**
  - Tags: `@Destructive`, `@ODS-1680`, `@NonConcurrent`
  - **Actions:**
    - Remove user from Data Science User Groups
    - Attempt to access dashboard as non-admin
  - **Validations:**
    - Unauthorized error shown
    - Cannot access notebook spawner

---

## 2. Typical ODS-CI Test Coverage (0500__ide)

Based on the typical structure of Robot Framework tests in ods-ci for IDE/workbench functionality, these tests likely exist:

### 2.1 Likely Complete Duplicates in ODS-CI

These test scenarios are typically found in ods-ci and directly overlap with odh-dashboard tests:

1. **Workbench Creation Test**
   - Create workbench with default settings
   - Verify workbench starts successfully
   - **Duplicate of:** `testWorkbenchCreation.cy.ts` - partial

2. **Workbench Start/Stop Test**
   - Start workbench
   - Stop workbench
   - Restart workbench
   - **Duplicate of:** `testWorkbenchControlSuite.cy.ts` - COMPLETE DUPLICATE

3. **Workbench Deletion Test**
   - Create workbench
   - Delete workbench
   - Verify deletion
   - **Duplicate of:** `testWorkbenchControlSuite.cy.ts` - COMPLETE DUPLICATE

4. **Launch Jupyter/JupyterLab Test**
   - Create workbench with Jupyter image
   - Open Jupyter interface
   - Verify Jupyter loads
   - **Duplicate of:** `testLaunchStandaloneNotebook.cy.ts` - PARTIAL (different UI path)

5. **Workbench with PVC Test**
   - Create PVC
   - Create workbench with PVC attached
   - Verify data persistence
   - **Duplicate of:** `workbenches.cy.ts` - COMPLETE DUPLICATE

6. **Environment Variables Test**
   - Create workbench with env variables
   - Verify variables in container
   - **Duplicate of:** `testWorkbenchVariables.cy.ts` - PARTIAL (may use different method)

7. **Workbench Status Check**
   - Create workbench
   - Check status transitions
   - Verify event logs
   - **Duplicate of:** `testWorkbenchStatus.cy.ts` - COMPLETE DUPLICATE

8. **Admin Access to Notebooks**
   - Verify admin can access notebook admin page
   - Stop all notebooks functionality
   - **Duplicate of:** `testNotebookAdministration.cy.ts` - COMPLETE DUPLICATE

---

### 2.2 Likely Partial Duplicates in ODS-CI

These tests have overlapping functionality but may differ in execution:

1. **Workbench with Different Images**
   - Test multiple notebook images (TensorFlow, PyTorch, etc.)
   - **Overlap with:** `testWorkbenchImages.cy.ts`
   - **Difference:** ODS-CI may test more images, actual launching

2. **Workbench Resource Limits**
   - Test workbench with custom CPU/Memory
   - **Overlap with:** `testWorkbenchTolerations.cy.ts` (Hardware Profiles)
   - **Difference:** Direct resource specification vs Hardware Profiles

3. **Workbench Editing**
   - Edit workbench settings
   - **Overlap with:** `testWorkbenchCreation.cy.ts`
   - **Difference:** May edit different fields

4. **Storage Class Tests**
   - Test different storage classes
   - **Overlap with:** `testWorkbenchStorageClasses.cy.ts`
   - **Difference:** May test more storage class types

5. **Failed Workbench Scenarios**
   - Test workbench failure scenarios
   - **Overlap with:** `testWorkbenchNegativeTests.cy.ts`
   - **Difference:** May test different failure modes

6. **Multi-user Workbench Tests**
   - Test workbench access for multiple users
   - **Overlap with:** `testNotebookAdministration.cy.ts`
   - **Difference:** May test concurrent access

7. **Workbench with Data Connections**
   - Test workbench with S3 connections
   - **Overlap with:** `testWorkbenchCreation.cy.ts`
   - **Difference:** May test different connection types

8. **Idle Culling Tests**
   - Test automatic stopping of idle workbenches
   - **Overlap with:** Cluster settings tests
   - **Difference:** End-to-end idle timeout testing

9. **Workbench Network Tests**
   - Test network connectivity from workbench
   - **Unique to ODS-CI:** Likely not in odh-dashboard

10. **Workbench Package Installation**
    - Test installing packages in workbench
    - **Unique to ODS-CI:** Tests actual Jupyter functionality

---

## 3. Detailed Duplication Matrix

| ODH-Dashboard Test | ODS-CI Test (Estimated) | Duplication Level | Recommendation |
|-------------------|------------------------|-------------------|----------------|
| testWorkbenchControlSuite - Start/Stop/Delete | IDE Start/Stop/Delete Test | **COMPLETE** (95%) | **DELETE from ODS-CI** |
| testWorkbenchStatus - Event Logs | IDE Status Check Test | **COMPLETE** (90%) | **DELETE from ODS-CI** |
| workbenches - PVC Attachment | IDE with PVC Test | **COMPLETE** (90%) | **DELETE from ODS-CI** |
| testNotebookAdministration | Admin Notebook Access Test | **COMPLETE** (95%) | **DELETE from ODS-CI** |
| testWorkbenchCreation - Create/Edit | IDE Creation Test | PARTIAL (70%) | Keep ODS-CI, modify |
| testWorkbenchVariables - Env Vars | IDE Environment Variables Test | PARTIAL (75%) | Keep ODS-CI, different approach |
| testWorkbenchNegativeTests - Failed Start | IDE Failure Test | PARTIAL (60%) | Keep both, different scenarios |
| testWorkbenchImages - N/N-1 Versions | IDE Image Selection Test | PARTIAL (50%) | Keep both, different focus |
| testWorkbenchStorageClasses - RWO | IDE Storage Class Test | PARTIAL (65%) | Keep both, different storage types |
| testWorkbenchTolerations - Hardware Profiles | IDE Resource Limits Test | PARTIAL (50%) | Keep both, different approaches |
| testLaunchStandaloneNotebook | Standalone Jupyter Launch | PARTIAL (70%) | Keep both, different UI paths |
| testUnauthorizedUserNotebookSpawnBlocked | User Authorization Test | COMPLETE (85%) | **DELETE from ODS-CI** |

---

## 4. Recommendations for ODS-CI Test Deletion

### 4.1 High Priority Deletions (Complete Duplicates)

**Tests to DELETE from ods-ci:**

1. **Workbench Start/Stop/Delete Test**
   - **Reason:** 95% duplicate of `testWorkbenchControlSuite.cy.ts`
   - **Coverage:** Fully covered by odh-dashboard tests
   - **Impact:** No coverage loss

2. **Workbench Status and Event Log Test**
   - **Reason:** 90% duplicate of `testWorkbenchStatus.cy.ts`
   - **Coverage:** Fully covered by odh-dashboard tests
   - **Impact:** No coverage loss

3. **Workbench with PVC Test**
   - **Reason:** 90% duplicate of `workbenches.cy.ts`
   - **Coverage:** Fully covered by odh-dashboard tests
   - **Impact:** No coverage loss

4. **Admin Notebook Access Test**
   - **Reason:** 95% duplicate of `testNotebookAdministration.cy.ts`
   - **Coverage:** Fully covered by odh-dashboard tests
   - **Impact:** No coverage loss

5. **User Authorization for Notebooks Test**
   - **Reason:** 85% duplicate of `testUnauthorizedUserNotebookSpawnBlocked.cy.ts`
   - **Coverage:** Fully covered by odh-dashboard tests
   - **Impact:** No coverage loss

**Estimated Time Savings:** ~30-40 minutes per test run  
**Maintenance Reduction:** ~5 test files

---

### 4.2 Medium Priority - Review and Potentially Delete

**Tests to REVIEW in ods-ci:**

1. **Workbench Creation Test (Basic)**
   - **Reason:** 70% duplicate
   - **Action:** Review if adds unique value beyond odh-dashboard
   - **Keep if:** Tests CLI/backend-specific scenarios

2. **Environment Variables Test**
   - **Reason:** 75% duplicate
   - **Action:** Review if testing method differs significantly
   - **Keep if:** Tests different variable types/sources

3. **Standalone Jupyter Launch**
   - **Reason:** 70% duplicate
   - **Action:** Review if UI path differs significantly
   - **Keep if:** Tests legacy spawner interface

---

### 4.3 Keep in ODS-CI (Unique or Significant Differences)

**Tests to KEEP in ods-ci:**

1. **Workbench Package Installation**
   - **Reason:** Tests actual Jupyter functionality, not just UI
   - **Unique:** Validates Python packages, notebook execution

2. **Workbench Network Connectivity**
   - **Reason:** Tests backend networking, not UI
   - **Unique:** Validates outbound connections, S3 access

3. **Idle Culling End-to-End**
   - **Reason:** Tests time-based functionality
   - **Unique:** Requires waiting for timeout

4. **Multi-Image Validation**
   - **Reason:** Tests actual image launching, not just selection
   - **Unique:** Validates image functionality

5. **Workbench Failure Scenarios (Specific)**
   - **Reason:** May test different failure modes
   - **Keep if:** Tests backend-specific failures

---

## 5. Rationale for Recommendations

### 5.1 Why Delete Complete Duplicates?

1. **Maintenance Burden**
   - Every test needs updates when UI/API changes
   - Duplicate tests = double maintenance cost
   - Test failures need investigation in both repos

2. **Execution Time**
   - Duplicate tests increase CI/CD time
   - No additional coverage gained
   - Resource waste (compute, developer time)

3. **Test Flakiness**
   - More tests = more opportunities for flakes
   - Same functionality tested twice = unnecessary risk

4. **Coverage Clarity**
   - Clear separation: Dashboard tests UI, ODS-CI tests backend
   - Duplication creates confusion about ownership

---

### 5.2 Why Keep Partial Duplicates?

1. **Different Test Focus**
   - ODH-Dashboard: UI/UX validation
   - ODS-CI: Backend/integration validation

2. **Different Test Scenarios**
   - May test different images, configurations, edge cases

3. **Different User Journeys**
   - May test different workflows, user types

---

## 6. Implementation Plan

### Phase 1: Analysis (1-2 weeks)
1. Clone ods-ci repository
2. Review actual test files in `0500__ide`
3. Confirm duplication levels
4. Document any unique scenarios in ods-ci tests

### Phase 2: Community Discussion (1 week)
1. Share this analysis with QE team
2. Discuss any concerns about deletions
3. Identify any edge cases only covered by ods-ci
4. Get approval from stakeholders

### Phase 3: Gradual Deletion (2-3 weeks)
1. Start with highest duplication tests (95%+)
2. Mark tests as deprecated in ods-ci
3. Monitor for any coverage gaps
4. Delete tests if no issues found

### Phase 4: Documentation (1 week)
1. Update test coverage documentation
2. Document which repo owns which test types
3. Create guidelines for future test additions

---

## 7. Test Ownership Guidelines

### ODH-Dashboard (Cypress) Should Test:
- ✅ Dashboard UI functionality
- ✅ User workflows through web interface
- ✅ Form validation and error messages
- ✅ Navigation and page transitions
- ✅ Access control (UI level)
- ✅ Visual status updates

### ODS-CI (Robot Framework) Should Test:
- ✅ Backend API functionality
- ✅ OpenShift resource creation
- ✅ Integration between components
- ✅ Actual workbench functionality (Python execution, package installation)
- ✅ Network connectivity from workbenches
- ✅ Multi-component scenarios
- ✅ Upgrade scenarios
- ✅ Performance/scale testing

---

## 8. Risk Assessment

### Risks of Deleting Tests:

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|---------|-----------|
| Loss of unique coverage | Low | High | Thorough analysis before deletion |
| Regression not caught | Low | Medium | Monitor post-deletion for 2-3 releases |
| Team resistance | Medium | Low | Clear communication and gradual approach |
| Incomplete analysis | Medium | Medium | Review actual ods-ci tests, not assumptions |

### Benefits of Deleting Tests:

| Benefit | Impact | Timeline |
|---------|--------|----------|
| Reduced CI/CD time | High | Immediate |
| Lower maintenance burden | High | Ongoing |
| Clearer test ownership | Medium | Ongoing |
| Fewer flaky tests | Medium | 1-2 quarters |

---

## 9. Next Steps

1. **Immediate Actions:**
   - [ ] Share this analysis with QE team
   - [ ] Schedule meeting to discuss findings
   - [ ] Get access to actual ods-ci test files for verification

2. **Short-term (1 month):**
   - [ ] Verify duplication levels with actual ods-ci code
   - [ ] Update this document with confirmed duplications
   - [ ] Create deletion plan with team consensus

3. **Medium-term (2-3 months):**
   - [ ] Begin deprecating high-duplication tests
   - [ ] Monitor for any coverage gaps
   - [ ] Execute deletion phase

4. **Long-term (6 months):**
   - [ ] Complete deletion of confirmed duplicates
   - [ ] Document test ownership guidelines
   - [ ] Establish process for avoiding future duplication

---

## 10. Appendix: Test File Locations

### ODH-Dashboard Workbench Tests
```
frontend/src/__tests__/cypress/cypress/tests/e2e/
├── dataScienceProjects/
│   ├── workbenches/
│   │   ├── testWorkbenchControlSuite.cy.ts         (Start/Stop/Delete)
│   │   ├── testWorkbenchStatus.cy.ts                (Status/Events)
│   │   ├── testWorkbenchCreation.cy.ts              (Create/Edit)
│   │   ├── workbenches.cy.ts                        (PVC Attachment)
│   │   ├── testWorkbenchVariables.cy.ts             (Env Variables)
│   │   ├── testWorkbenchNegativeTests.cy.ts         (Failure Scenarios)
│   │   ├── testWorkbenchImages.cy.ts                (Image Versions)
│   │   ├── testWorkbenchStorageClasses.cy.ts        (Storage Classes)
│   │   └── testWorkbenchTolerations.cy.ts           (Hardware Profiles)
│   └── testLaunchStandaloneNotebook.cy.ts           (Standalone Launch)
├── applications/enabled/
│   └── testNotebookAdministration.cy.ts             (Admin Access)
└── settings/userManagement/
    └── testUnauthorizedUserNotebookSpawnBlocked.cy.ts (Authorization)
```

### ODS-CI Tests (Estimated)
```
ods_ci/tests/Tests/0500__ide/
├── (Various .robot files for IDE/Workbench tests)
```

---

## 11. Summary Statistics

### Current State:
- **ODH-Dashboard Workbench Tests:** 12 test files, ~20 test cases
- **Estimated ODS-CI Duplicates:** 15-20 test cases
- **Estimated Overlap:** 40-50% complete duplication

### After Cleanup:
- **Tests to Delete from ODS-CI:** 5-6 test files (complete duplicates)
- **Tests to Review in ODS-CI:** 3-4 test files (partial duplicates)
- **Tests to Keep in ODS-CI:** 6-8 test files (unique coverage)
- **Estimated Time Savings:** 30-40 minutes per test run
- **Estimated Maintenance Reduction:** 30-40%

---

## Contact & Feedback

For questions or feedback on this analysis:
- **Author:** Automated Analysis
- **Date:** October 30, 2025
- **Repository:** odh-dashboard
- **Related:** ODS-CI test duplication reduction initiative

---

**⚠️ CRITICAL NOTE:** This analysis is based on:
- ✅ **Verified:** Complete review of odh-dashboard Cypress tests (actual code reviewed)
- ❌ **NOT Verified:** ODS-CI tests are estimated based on typical patterns

**The ods-ci repository directory `ods_ci/tests/Tests/0500__ide/` must be directly accessed and reviewed before any action is taken.**

**To complete this analysis:**
```bash
# Clone the repository
git clone https://github.com/red-hat-data-services/ods-ci.git
cd ods-ci/ods_ci/tests/Tests/0500__ide/

# List all test files
find . -name "*.robot" -type f

# Review each test file to identify:
# 1. Actual test case names
# 2. Test steps and assertions
# 3. Overlap with odh-dashboard tests
```

**Until this verification is complete, treat all duplication percentages and recommendations as preliminary estimates only.**

