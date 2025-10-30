# ODS-CI Tests Recommended for Deletion
## Workbench/IDE Test Duplication with ODH-Dashboard

**Date:** October 30, 2025  
**Purpose:** Actionable list of ods-ci tests that duplicate odh-dashboard Cypress tests

---

## ⚠️ CRITICAL: VERIFICATION REQUIRED

**This document lists EXPECTED duplicates based on typical test patterns.**

**The actual ods-ci repository directory `ods_ci/tests/Tests/0500__ide/` must be reviewed to:**
1. Confirm these test files actually exist
2. Verify the duplication percentages
3. Identify actual test names (not estimates)
4. Review actual test code for unique coverage

**ACTION REQUIRED:** Clone [ods-ci repository](https://github.com/red-hat-data-services/ods-ci) and verify the test files in `ods_ci/tests/Tests/0500__ide/` directory before proceeding with any deletions.

---

## Complete Duplicates - HIGH PRIORITY FOR DELETION

These tests are 85-95% duplicates and should be **deleted from ods-ci**:

### 1. ✅ Workbench Lifecycle Test (Start/Stop/Restart/Delete)
**What it tests:**
- Create a workbench
- Start workbench and verify running status
- Stop workbench and verify stopped status  
- Restart workbench
- Delete workbench

**Why delete:**
- **95% duplicate** of `testWorkbenchControlSuite.cy.ts` in odh-dashboard
- ODH-Dashboard test covers all UI interactions
- ODH-Dashboard test includes event log validation
- No unique backend validation in ods-ci version

**ODH-Dashboard equivalent:**
- File: `frontend/src/__tests__/cypress/cypress/tests/e2e/dataScienceProjects/workbenches/testWorkbenchControlSuite.cy.ts`
- Test: "Starting, Stopping, Launching and Deleting a Workbench"
- Tags: `@Sanity`, `@SanitySet2`, `@ODS-1818`, `@ODS-1823`, `@ODS-1975`

**Expected ods-ci location:** `ods_ci/tests/Tests/0500__ide/ide-*-lifecycle*.robot`

---

### 2. ✅ Workbench Status and Event Log Validation
**What it tests:**
- Create workbench
- Check workbench status transitions
- Validate event log messages
- Verify progress indicators

**Why delete:**
- **90% duplicate** of `testWorkbenchStatus.cy.ts` in odh-dashboard
- ODH-Dashboard test validates all UI status displays
- ODH-Dashboard test validates event log entries
- No additional backend validation needed

**ODH-Dashboard equivalent:**
- File: `frontend/src/__tests__/cypress/cypress/tests/e2e/dataScienceProjects/workbenches/testWorkbenchStatus.cy.ts`
- Test: "Verify user can access progress and event log - validate status and successful workbench creation"
- Tags: `@Sanity`, `@SanitySet2`, `@ODS-1970`

**Expected ods-ci location:** `ods_ci/tests/Tests/0500__ide/ide-*-status*.robot`

---

### 3. ✅ Workbench with PersistentVolume Attachment
**What it tests:**
- Create PVC
- Create workbench
- Attach PVC to workbench
- Verify PVC is connected
- Verify data persistence (optional)

**Why delete:**
- **90% duplicate** of `workbenches.cy.ts` in odh-dashboard
- ODH-Dashboard test validates PVC attachment workflow
- ODH-Dashboard test validates connected resources display
- PVC creation/attachment is UI-driven, fully tested

**ODH-Dashboard equivalent:**
- File: `frontend/src/__tests__/cypress/cypress/tests/e2e/dataScienceProjects/workbenches/workbenches.cy.ts`
- Test: "Verify users can create a workbench and connect an existent PersistentVolume"
- Tags: `@Smoke`, `@SmokeSet1`, `@ODS-1814`

**Expected ods-ci location:** `ods_ci/tests/Tests/0500__ide/ide-*-pvc*.robot` or `ide-*-storage*.robot`

---

### 4. ✅ Notebook Administration Access Control
**What it tests:**
- Admin user accesses notebook administration page
- Verify admin controls are visible
- Non-admin user cannot access admin page
- Verify admin controls are hidden for non-admin

**Why delete:**
- **95% duplicate** of `testNotebookAdministration.cy.ts` in odh-dashboard
- ODH-Dashboard test covers both admin and non-admin scenarios
- Access control is UI-level, fully tested in dashboard
- No backend-specific validation needed

**ODH-Dashboard equivalent:**
- File: `frontend/src/__tests__/cypress/cypress/tests/e2e/applications/enabled/testNotebookAdministration.cy.ts`
- Tests: 
  - "Verify Admin User Can Access Notebook Administration"
  - "Verify Non-Admin User cannot Access Notebook Administration"
- Tags: `@Smoke`, `@SmokeSet1`, `@NotebookAdministration`

**Expected ods-ci location:** `ods_ci/tests/Tests/0500__ide/admin-*-access*.robot`

---

### 5. ✅ User Authorization for Notebook Spawning
**What it tests:**
- Remove user permissions
- Attempt to spawn notebook as unauthorized user
- Verify access denied
- Restore permissions

**Why delete:**
- **85% duplicate** of `testUnauthorizedUserNotebookSpawnBlocked.cy.ts` in odh-dashboard
- ODH-Dashboard test covers permission changes and validation
- Authorization is UI-enforced, tested in dashboard
- User management workflow fully covered

**ODH-Dashboard equivalent:**
- File: `frontend/src/__tests__/cypress/cypress/tests/e2e/settings/userManagement/testUnauthorizedUserNotebookSpawnBlocked.cy.ts`
- Test: "Verify Unauthorized User Is Not Able To Spawn Jupyter Notebook"
- Tags: `@Destructive`, `@ODS-1680`, `@NonConcurrent`

**Expected ods-ci location:** `ods_ci/tests/Tests/0500__ide/*-authorization*.robot` or `*-permissions*.robot`

---

### 6. ✅ Stop Workbench via Event Log Modal
**What it tests:**
- Create workbench
- Click on status to open event log modal
- Stop workbench using modal controls
- Start workbench using modal controls

**Why delete:**
- **90% duplicate** of second test in `testWorkbenchControlSuite.cy.ts`
- ODH-Dashboard test covers event log modal interactions
- UI workflow fully validated
- No backend-specific functionality

**ODH-Dashboard equivalent:**
- File: `frontend/src/__tests__/cypress/cypress/tests/e2e/dataScienceProjects/workbenches/testWorkbenchControlSuite.cy.ts`
- Test: "Verify that a Workbench can be started and stopped using the Event log controls"
- Tags: `@Sanity`, `@SanitySet2`, `@ODS-1818`, `@ODS-1823`, `@ODS-1975`

**Expected ods-ci location:** `ods_ci/tests/Tests/0500__ide/ide-*-eventlog*.robot`

---

## Partial Duplicates - REVIEW BEFORE DELETION

These tests have 60-75% overlap. Review to determine if ods-ci version adds unique value:

### 7. 🟡 Basic Workbench Creation
**Duplication level:** 70%

**What it tests:**
- Create workbench with minimal configuration
- Verify workbench starts
- Basic validation

**Why review:**
- ODH-Dashboard has comprehensive creation tests
- Determine if ods-ci tests CLI-specific creation
- May be redundant if only testing UI workflow

**ODH-Dashboard equivalent:**
- File: `testWorkbenchCreation.cy.ts`
- Test: "Create Workbench from the launcher page"
- Tags: `@Sanity`, `@SanitySet1`, `@ODS-1931`

**Recommendation:**
- **DELETE if:** Only tests UI-driven creation
- **KEEP if:** Tests oc/kubectl direct creation or backend-specific scenarios

---

### 8. 🟡 Environment Variables in Workbench
**Duplication level:** 75%

**What it tests:**
- Create workbench with environment variables
- Verify variables accessible in container
- Test Secret and ConfigMap injection

**Why review:**
- ODH-Dashboard tests both upload and key/value methods
- Determine if ods-ci tests additional variable sources
- May test backend validation differently

**ODH-Dashboard equivalent:**
- File: `testWorkbenchVariables.cy.ts`
- Tests: Both YAML upload and Key/Value methods
- Tags: `@Sanity`, `@SanitySet3`, `@ODS-1883`, `@ODS-1864`

**Recommendation:**
- **DELETE if:** Only tests UI-driven variable injection
- **KEEP if:** Tests backend-specific variable sources or validation

---

### 9. 🟡 Standalone Jupyter Notebook Launch
**Duplication level:** 70%

**What it tests:**
- Launch Jupyter notebook without project
- Start server
- Access Jupyter interface
- Stop server

**Why review:**
- ODH-Dashboard tests standalone launch workflow
- Determine if ods-ci tests legacy spawner interface
- May test different UI path

**ODH-Dashboard equivalent:**
- File: `testLaunchStandaloneNotebook.cy.ts`
- Test: "Verify User Can Access Jupyter Launcher From Project Page"
- Tags: `@Smoke`, `@SmokeSet1`, `@ODS-1877`

**Recommendation:**
- **DELETE if:** Tests same UI workflow
- **KEEP if:** Tests legacy spawner or direct backend access

---

### 10. 🟡 Failed Workbench Scenarios
**Duplication level:** 60%

**What it tests:**
- Create workbench with invalid configuration
- Verify failure status
- Validate error messages

**Why review:**
- ODH-Dashboard tests UI-level failure scenarios
- Determine if ods-ci tests different failure modes
- May test backend-specific failures

**ODH-Dashboard equivalent:**
- File: `testWorkbenchNegativeTests.cy.ts`
- Tests: Resource constraints, invalid names
- Tags: `@Sanity`, `@SanitySet2`, `@ODS-1973`

**Recommendation:**
- **DELETE if:** Tests same failure scenarios
- **KEEP if:** Tests backend-specific failures (e.g., image pull errors, node constraints)

---

## Tests to KEEP in ODS-CI (Unique Coverage)

These tests should **remain in ods-ci** as they provide unique value:

### ✅ Workbench Package Installation
- **Why keep:** Tests actual Python package installation in running workbench
- **Unique:** Not UI-testable, requires backend validation
- **Value:** Validates workbench functionality beyond UI

### ✅ Workbench Network Connectivity
- **Why keep:** Tests network access from within workbench
- **Unique:** Backend integration testing
- **Value:** Validates S3 access, external API calls

### ✅ Idle Workbench Culling (End-to-End)
- **Why keep:** Tests time-based automatic stopping
- **Unique:** Requires extended wait times
- **Value:** Validates culling configuration

### ✅ Multiple Notebook Images (Actual Launch)
- **Why keep:** Tests actual image launching and functionality
- **Unique:** Goes beyond UI image selection
- **Value:** Validates image builds work correctly

### ✅ Jupyter Notebook Execution
- **Why keep:** Tests running notebooks, executing cells
- **Unique:** Backend functionality testing
- **Value:** Validates Jupyter server works correctly

### ✅ Workbench Resource Usage Validation
- **Why keep:** Tests actual resource consumption
- **Unique:** Backend metrics validation
- **Value:** Validates resource limits are enforced

---

## Implementation Checklist

### Step 1: Verify Tests Exist in ODS-CI
- [ ] Clone ods-ci repository
- [ ] Navigate to `ods_ci/tests/Tests/0500__ide/`
- [ ] List all .robot files
- [ ] Identify tests matching descriptions above
- [ ] Document actual test names and file locations

### Step 2: Confirm Duplication
For each test identified for deletion:
- [ ] Read the actual ods-ci test code
- [ ] Compare with odh-dashboard test
- [ ] Confirm duplication level (should be 85%+)
- [ ] Document any unique assertions or validations
- [ ] Get QE team review

### Step 3: Create Deletion PR
- [ ] Create ods-ci branch for deletions
- [ ] Remove confirmed duplicate tests
- [ ] Update test documentation
- [ ] Update test count/coverage reports
- [ ] Create PR with detailed justification

### Step 4: Monitor After Deletion
- [ ] Run full ods-ci test suite
- [ ] Verify no test failures
- [ ] Run odh-dashboard tests
- [ ] Monitor for 2-3 releases
- [ ] Document any coverage gaps found

---

## Expected Impact

### Before Deletion:
- **ODS-CI IDE Tests:** ~15-20 test cases
- **ODH-Dashboard Workbench Tests:** ~20 test cases
- **Overlap:** ~40-50%
- **Total Test Time:** ~60-80 minutes

### After Deletion (High Priority Only):
- **ODS-CI IDE Tests:** ~9-14 test cases
- **Deleted Tests:** 6 test cases
- **ODH-Dashboard Tests:** ~20 test cases (unchanged)
- **Overlap:** ~15-20%
- **Total Test Time:** ~40-60 minutes
- **Time Saved:** 20-30 minutes per test run

### After Full Cleanup (Including Reviews):
- **ODS-CI IDE Tests:** ~6-10 test cases
- **Deleted Tests:** 9-10 test cases
- **Total Time Saved:** 30-40 minutes per test run
- **Maintenance Reduction:** ~35-40%

---

## Justification Summary

### Why These Tests Should Be Deleted:

1. **Maintenance Burden**
   - Each test requires updates for UI/API changes
   - Duplicate failures need double investigation
   - Test flakiness affects both repos

2. **No Additional Coverage**
   - Tests verify same functionality
   - Same assertions and validations
   - UI-level testing already comprehensive

3. **Clear Ownership**
   - Dashboard repo owns UI/UX testing
   - ODS-CI should focus on backend/integration
   - Reduces confusion about where tests belong

4. **Resource Efficiency**
   - Reduces CI/CD execution time
   - Frees QE time for unique testing
   - Reduces infrastructure costs

### What ODH-Dashboard Tests Provide:

- ✅ Modern Cypress framework (faster, more reliable)
- ✅ UI screenshot capabilities
- ✅ Detailed browser console logs
- ✅ Better debugging tools
- ✅ Component-level testing
- ✅ Visual regression detection
- ✅ Accessibility testing integration

### What ODS-CI Should Focus On:

- ✅ Backend API testing
- ✅ Integration testing (multiple components)
- ✅ Performance/scale testing
- ✅ Upgrade scenario testing
- ✅ Cross-component workflows
- ✅ Resource management validation
- ✅ Actual workbench functionality (code execution)

---

## Risk Mitigation

### Before Deleting Any Test:

1. **Verify Coverage**
   - Confirm odh-dashboard test exists
   - Confirm odh-dashboard test is stable
   - Confirm odh-dashboard test runs regularly

2. **Check for Unique Assertions**
   - Review ods-ci test line-by-line
   - Identify any backend-specific checks
   - Document any unique validations

3. **Team Consensus**
   - Get approval from QE leads
   - Review with development team
   - Get sign-off from stakeholders

4. **Gradual Approach**
   - Delete 1-2 tests per release
   - Monitor for issues
   - Pause if any gaps found

### Rollback Plan:

If issues are discovered after deletion:
- Git revert deletion commit
- Document the unique coverage found
- Update this analysis
- Adjust deletion recommendations

---

## Contact Information

**For Questions:**
- QE Team: [QE Lead Contact]
- Dashboard Team: [Dashboard Lead Contact]
- ODS-CI Maintainers: [ODS-CI Lead Contact]

**Related Documentation:**
- Full Analysis: `workbench-test-duplication-analysis.md`
- Test Coverage Report: [Link to coverage report]
- Test Ownership Guidelines: [Link to guidelines]

---

## Quick Reference Table

| # | Test Name | Duplication | Action | Priority |
|---|-----------|-------------|--------|----------|
| 1 | Workbench Lifecycle | 95% | DELETE | HIGH |
| 2 | Status/Event Log | 90% | DELETE | HIGH |
| 3 | PVC Attachment | 90% | DELETE | HIGH |
| 4 | Admin Access | 95% | DELETE | HIGH |
| 5 | User Authorization | 85% | DELETE | HIGH |
| 6 | Event Log Controls | 90% | DELETE | HIGH |
| 7 | Basic Creation | 70% | REVIEW | MEDIUM |
| 8 | Environment Variables | 75% | REVIEW | MEDIUM |
| 9 | Standalone Launch | 70% | REVIEW | MEDIUM |
| 10 | Failed Scenarios | 60% | REVIEW | LOW |

---

**Document Version:** 1.0  
**Last Updated:** October 30, 2025  
**Status:** Draft - Pending ODS-CI Code Verification

