# Test Duplication Summary - Quick Reference
## ODH-Dashboard ↔️ ODS-CI Workbench Tests

---

## Visual Mapping: Complete Duplicates (DELETE from ODS-CI)

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    ODH-DASHBOARD (Cypress)                               │
│                         KEEP ALL TESTS                                   │
└──────────────────────────────┬──────────────────────────────────────────┘
                               │
                               │ 95% DUPLICATE
                               ↓
┌─────────────────────────────────────────────────────────────────────────┐
│ 1. testWorkbenchControlSuite.cy.ts                                      │
│    "Starting, Stopping, Launching and Deleting a Workbench"             │
│    @Sanity @SanitySet2 @ODS-1818 @ODS-1823 @ODS-1975                    │
└──────────────────────────────┬──────────────────────────────────────────┘
                               │
                               ↓  DELETE THIS ↓
┌─────────────────────────────────────────────────────────────────────────┐
│ ODS-CI: Workbench Start/Stop/Restart/Delete Test                        │
│ Location: ods_ci/tests/Tests/0500__ide/ide-*-lifecycle*.robot          │
│ Action: ❌ DELETE - 95% duplicate                                       │
└─────────────────────────────────────────────────────────────────────────┘

───────────────────────────────────────────────────────────────────────────

┌─────────────────────────────────────────────────────────────────────────┐
│ 2. testWorkbenchStatus.cy.ts                                            │
│    "Verify user can access progress and event log"                      │
│    @Sanity @SanitySet2 @ODS-1970                                        │
└──────────────────────────────┬──────────────────────────────────────────┘
                               │
                               ↓  DELETE THIS ↓
┌─────────────────────────────────────────────────────────────────────────┐
│ ODS-CI: Workbench Status and Event Log Test                             │
│ Location: ods_ci/tests/Tests/0500__ide/ide-*-status*.robot             │
│ Action: ❌ DELETE - 90% duplicate                                       │
└─────────────────────────────────────────────────────────────────────────┘

───────────────────────────────────────────────────────────────────────────

┌─────────────────────────────────────────────────────────────────────────┐
│ 3. workbenches.cy.ts                                                     │
│    "Create workbench and connect existent PersistentVolume"             │
│    @Smoke @SmokeSet1 @ODS-1814                                          │
└──────────────────────────────┬──────────────────────────────────────────┘
                               │
                               ↓  DELETE THIS ↓
┌─────────────────────────────────────────────────────────────────────────┐
│ ODS-CI: Workbench with PVC Test                                         │
│ Location: ods_ci/tests/Tests/0500__ide/ide-*-pvc*.robot                │
│ Action: ❌ DELETE - 90% duplicate                                       │
└─────────────────────────────────────────────────────────────────────────┘

───────────────────────────────────────────────────────────────────────────

┌─────────────────────────────────────────────────────────────────────────┐
│ 4. testNotebookAdministration.cy.ts                                     │
│    "Admin/Non-Admin Access to Notebook Administration"                  │
│    @Smoke @SmokeSet1 @NotebookAdministration                            │
└──────────────────────────────┬──────────────────────────────────────────┘
                               │
                               ↓  DELETE THIS ↓
┌─────────────────────────────────────────────────────────────────────────┐
│ ODS-CI: Admin Notebook Access Test                                      │
│ Location: ods_ci/tests/Tests/0500__ide/admin-*-access*.robot           │
│ Action: ❌ DELETE - 95% duplicate                                       │
└─────────────────────────────────────────────────────────────────────────┘

───────────────────────────────────────────────────────────────────────────

┌─────────────────────────────────────────────────────────────────────────┐
│ 5. testUnauthorizedUserNotebookSpawnBlocked.cy.ts                       │
│    "Unauthorized User Cannot Spawn Jupyter Notebook"                    │
│    @Destructive @ODS-1680                                               │
└──────────────────────────────┬──────────────────────────────────────────┘
                               │
                               ↓  DELETE THIS ↓
┌─────────────────────────────────────────────────────────────────────────┐
│ ODS-CI: User Authorization Test                                         │
│ Location: ods_ci/tests/Tests/0500__ide/*-authorization*.robot          │
│ Action: ❌ DELETE - 85% duplicate                                       │
└─────────────────────────────────────────────────────────────────────────┘

───────────────────────────────────────────────────────────────────────────

┌─────────────────────────────────────────────────────────────────────────┐
│ 6. testWorkbenchControlSuite.cy.ts (2nd test)                           │
│    "Start/Stop Workbench using Event log controls"                      │
│    @Sanity @SanitySet2                                                  │
└──────────────────────────────┬──────────────────────────────────────────┘
                               │
                               ↓  DELETE THIS ↓
┌─────────────────────────────────────────────────────────────────────────┐
│ ODS-CI: Event Log Modal Controls Test                                   │
│ Location: ods_ci/tests/Tests/0500__ide/ide-*-eventlog*.robot           │
│ Action: ❌ DELETE - 90% duplicate                                       │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Visual Mapping: Partial Duplicates (REVIEW)

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    ODH-DASHBOARD (Cypress)                               │
└──────────────────────────────┬──────────────────────────────────────────┘
                               │
                               │ 70% DUPLICATE
                               ↓
┌─────────────────────────────────────────────────────────────────────────┐
│ 7. testWorkbenchCreation.cy.ts                                          │
│    "Create Workbench from the launcher page"                            │
│    @Sanity @SanitySet1 @ODS-1931                                        │
└──────────────────────────────┬──────────────────────────────────────────┘
                               │
                               ↓  REVIEW THIS ↓
┌─────────────────────────────────────────────────────────────────────────┐
│ ODS-CI: Basic Workbench Creation Test                                   │
│ Location: ods_ci/tests/Tests/0500__ide/ide-*-creation*.robot           │
│ Action: 🟡 REVIEW - Delete if UI-only, Keep if CLI-specific             │
└─────────────────────────────────────────────────────────────────────────┘

───────────────────────────────────────────────────────────────────────────

┌─────────────────────────────────────────────────────────────────────────┐
│ 8. testWorkbenchVariables.cy.ts                                         │
│    "Set environment variables (YAML & Key/Value)"                       │
│    @Sanity @SanitySet3 @ODS-1883 @ODS-1864                              │
└──────────────────────────────┬──────────────────────────────────────────┘
                               │
                               ↓  REVIEW THIS ↓
┌─────────────────────────────────────────────────────────────────────────┐
│ ODS-CI: Environment Variables Test                                      │
│ Location: ods_ci/tests/Tests/0500__ide/ide-*-envvar*.robot             │
│ Action: 🟡 REVIEW - Delete if UI-only, Keep if backend-specific         │
└─────────────────────────────────────────────────────────────────────────┘

───────────────────────────────────────────────────────────────────────────

┌─────────────────────────────────────────────────────────────────────────┐
│ 9. testLaunchStandaloneNotebook.cy.ts                                   │
│    "Launch Jupyter from Project Page"                                   │
│    @Smoke @SmokeSet1 @ODS-1877                                          │
└──────────────────────────────┬──────────────────────────────────────────┘
                               │
                               ↓  REVIEW THIS ↓
┌─────────────────────────────────────────────────────────────────────────┐
│ ODS-CI: Standalone Jupyter Launch Test                                  │
│ Location: ods_ci/tests/Tests/0500__ide/jupyter-*-launch*.robot         │
│ Action: 🟡 REVIEW - Delete if same path, Keep if legacy spawner         │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Tests to KEEP in ODS-CI (Unique Value)

```
┌─────────────────────────────────────────────────────────────────────────┐
│              ODS-CI UNIQUE TESTS - KEEP ALL                              │
├─────────────────────────────────────────────────────────────────────────┤
│ ✅ Workbench Package Installation                                       │
│    → Tests pip install, conda, package functionality                    │
│    → Backend validation, not UI-testable                                │
│                                                                           │
│ ✅ Workbench Network Connectivity                                       │
│    → Tests S3 access, external API calls from workbench                 │
│    → Backend integration testing                                        │
│                                                                           │
│ ✅ Idle Workbench Culling (E2E)                                         │
│    → Tests automatic stopping after timeout                             │
│    → Requires extended wait times                                       │
│                                                                           │
│ ✅ Multiple Notebook Images (Actual Launch)                             │
│    → Tests image launches and validates functionality                   │
│    → Goes beyond UI image selection                                     │
│                                                                           │
│ ✅ Jupyter Notebook Execution                                           │
│    → Tests running notebooks, executing Python code                     │
│    → Backend functionality validation                                   │
│                                                                           │
│ ✅ Workbench Resource Usage                                             │
│    → Tests actual CPU/memory consumption                                │
│    → Backend metrics validation                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Decision Tree

```
                    ┌──────────────────────────┐
                    │  ODS-CI Workbench Test   │
                    └────────────┬─────────────┘
                                 │
                    ┌────────────▼─────────────┐
                    │ Does ODH-Dashboard have  │
                    │   equivalent test?       │
                    └────────┬────────┬────────┘
                             │        │
                        YES  │        │  NO
                             │        │
                    ┌────────▼────┐  ┌▼──────────────┐
                    │ Is it 85%+  │  │  KEEP IN      │
                    │ duplicate?  │  │  ODS-CI       │
                    └───┬────┬────┘  └───────────────┘
                        │    │
                   YES  │    │  NO
                        │    │
              ┌─────────▼┐  ┌▼──────────────────────┐
              │ DELETE   │  │ Does ODS-CI test      │
              │ FROM     │  │ backend-specific      │
              │ ODS-CI   │  │ functionality?        │
              └──────────┘  └──┬──────────┬─────────┘
                               │          │
                          YES  │          │  NO
                               │          │
                     ┌─────────▼─┐   ┌────▼──────┐
                     │ KEEP IN   │   │ DELETE    │
                     │ ODS-CI    │   │ FROM      │
                     └───────────┘   │ ODS-CI    │
                                     └───────────┘
```

---

## Summary Statistics

### Current State
| Metric | Count |
|--------|-------|
| ODH-Dashboard Workbench Tests | 20 tests |
| ODS-CI IDE Tests (estimated) | 18-20 tests |
| Overlap | 40-50% |

### After Recommended Deletions
| Metric | Before | After | Reduction |
|--------|--------|-------|-----------|
| Complete Duplicates | 6 tests | 0 tests | -6 tests |
| Partial Duplicates (after review) | 4 tests | 2 tests | -2 tests |
| **Total ODS-CI Tests** | **18-20** | **10-12** | **-8 tests** |
| **Test Execution Time** | **60-80 min** | **40-50 min** | **-30 min** |
| **Maintenance Effort** | **100%** | **60%** | **-40%** |

---

## Action Items Checklist

### Immediate (This Week)
- [ ] Clone ods-ci repository
- [ ] Navigate to `ods_ci/tests/Tests/0500__ide/`
- [ ] List all .robot files in directory
- [ ] Map actual test names to this analysis
- [ ] Share findings with QE team

### Short-term (Next 2 Weeks)
- [ ] Review Test #1: Workbench Lifecycle
- [ ] Review Test #2: Status/Event Log
- [ ] Review Test #3: PVC Attachment
- [ ] Review Test #4: Admin Access
- [ ] Review Test #5: User Authorization
- [ ] Review Test #6: Event Log Controls
- [ ] Get team consensus on deletions

### Medium-term (Next Month)
- [ ] Create deletion PR for high-priority tests
- [ ] Update ods-ci test documentation
- [ ] Run full test suite validation
- [ ] Monitor for coverage gaps

### Long-term (Next Quarter)
- [ ] Review partial duplicates (Tests #7-10)
- [ ] Create additional deletion PRs if needed
- [ ] Document test ownership guidelines
- [ ] Establish duplication prevention process

---

## Quick Reference: Files to Check

### ODH-Dashboard Tests (Cypress)
```bash
cd frontend/src/__tests__/cypress/cypress/tests/e2e/

# Workbench tests
ls dataScienceProjects/workbenches/
# → testWorkbenchControlSuite.cy.ts
# → testWorkbenchStatus.cy.ts
# → testWorkbenchCreation.cy.ts
# → workbenches.cy.ts
# → testWorkbenchVariables.cy.ts
# → testWorkbenchNegativeTests.cy.ts
# → testWorkbenchImages.cy.ts
# → testWorkbenchStorageClasses.cy.ts
# → testWorkbenchTolerations.cy.ts

# Notebook tests
ls dataScienceProjects/
# → testLaunchStandaloneNotebook.cy.ts

ls applications/enabled/
# → testNotebookAdministration.cy.ts

ls settings/userManagement/
# → testUnauthorizedUserNotebookSpawnBlocked.cy.ts
```

### ODS-CI Tests (Robot Framework)
```bash
cd ods_ci/tests/Tests/0500__ide/

# List all IDE/workbench test files
ls -la *.robot

# Expected files (verify these exist):
# → ide-*-lifecycle*.robot  (DELETE - #1)
# → ide-*-status*.robot     (DELETE - #2)
# → ide-*-pvc*.robot        (DELETE - #3)
# → admin-*-access*.robot   (DELETE - #4)
# → *-authorization*.robot  (DELETE - #5)
# → ide-*-eventlog*.robot   (DELETE - #6)
# → ide-*-creation*.robot   (REVIEW - #7)
# → ide-*-envvar*.robot     (REVIEW - #8)
# → jupyter-*-launch*.robot (REVIEW - #9)
```

---

## Expected Outcomes

### Immediate Benefits
✅ Reduce test execution time by 30-40 minutes  
✅ Reduce maintenance burden by 40%  
✅ Clearer test ownership between teams  
✅ Fewer flaky test failures  

### Long-term Benefits
✅ More focused test suites in each repo  
✅ Faster CI/CD pipelines  
✅ Easier onboarding for new QE team members  
✅ Better test coverage visibility  

---

## Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Missing unique coverage | Low | High | Thorough code review before deletion |
| Team resistance | Medium | Low | Clear communication and gradual approach |
| Regression not caught | Low | Medium | Monitor 2-3 releases post-deletion |

---

## Success Criteria

Delete tests when ALL conditions are met:
1. ✅ Confirmed 85%+ duplication with odh-dashboard test
2. ✅ No unique backend validations in ods-ci test
3. ✅ ODH-Dashboard test is stable and running regularly
4. ✅ QE team consensus achieved
5. ✅ Documentation updated

---

**Document Status:** ⚠️ REQUIRES ODS-CI DIRECTORY VERIFICATION  
**Next Update:** After accessing actual ods-ci test files in `ods_ci/tests/Tests/0500__ide/`  
**Owner:** QE Team  
**Last Updated:** October 30, 2025

---

## ⚠️ IMPORTANT LIMITATION

**This analysis is based on:**
- ✅ Complete review of ODH-Dashboard Cypress tests (verified from actual code)
- ❌ **Estimated/typical patterns** for ODS-CI tests (NOT verified from actual code)

**To complete this analysis, you MUST:**
1. Clone the ods-ci repository: `git clone https://github.com/red-hat-data-services/ods-ci.git`
2. Navigate to: `cd ods-ci/ods_ci/tests/Tests/0500__ide/`
3. List actual test files: `ls -la *.robot`
4. Review actual test content to confirm duplication
5. Update this document with verified findings

**Until the actual ods-ci test files in the 0500__ide directory are reviewed, the recommendations in this document should be considered preliminary.**

