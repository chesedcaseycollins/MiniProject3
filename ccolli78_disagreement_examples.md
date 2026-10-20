# Disagreement Examples — ccolli78 (Casey Collins) & bnoyes (Benjamin Noyes)

Validation logs: `ccolli78_validation_log.csv` (Casey validating Benjamin's MiniProject2) and `bnoyes_validation_log.csv` (Benjamin validating Casey's MiniProject2). All 24 disagreements and their resolutions are in `ccolli78_disagreement_resolution.csv`. The four below were picked because each one exposed a different kind of problem: a vocabulary gap, a rule-application ambiguity, evidence specificity, and snapshot drift.

## Example 1 — jackwasey_icd (HasRecovered)
**Project owner:** Casey Collins (ccolli78). **Validator:** Benjamin Noyes (bnoyes).
**Author:** Partially
**Validator:** No
**Evidence:** The longest gap is 36 months. Within the MiniProject2 data window the only commit after it is a single README update on 2024-12-20. A burst of commits fixing the package for modern R checks (PR #219, GitHub Actions replacing Travis/AppVeyor, R-hub v2) appears in 2026-09, after the data snapshot.
**Discussion:** Casey had written "Partially" to capture the one commit plus the later burst. Benjamin pointed out that the codebook only allows yes or no, and that a lone README edit after three years is not the project becoming active again. Casey agreed.
**Resolution:** ValidatorKept. Adjudicated value: No. Lesson: hedged labels outside the codebook vocabulary should be avoided, and the recovery judgement should use the same data window as the gap analysis.

## Example 2 — metagenome-atlas_atlas (Currentstatus)
**Project owner:** Benjamin Noyes (bnoyes). **Validator:** Casey Collins (ccolli78).
**Author:** Active
**Validator:** Inactive
**Evidence:** The codebook marks a project Inactive if its last commit is before 2025-04-01. Benjamin's own stats file records lastGHCommitDate as 2025-03-19, which is the last commit on the default branch `main`. The repository's pushed_at date is 2026-05-28, but every later push is on an unmerged side branch: WIP commits by the maintainer and a google-labs-jules bot documentation conversion. The same situation applied to opengeospatial_teamengine (last commit on `master` 2025-03-17, later pushes are unmerged dependabot branches).
**Discussion:** The real question was whether "last commit" means the default branch or any branch. We agreed on the default branch, since unmerged bot and WIP branches do not represent the project's released state. This also settled the mirror case in Benjamin's log, where jackwasey_icd had been marked Active by Casey because of commits made after the data window; under the agreed rule it is Inactive. scify_jedaitoolkit stays Active by the letter of the rule (a Dependabot bump was merged on 2025-07-12) even though the repository is archived, which we flagged as a codebook weakness.
**Resolution:** ValidatorKept for atlas, teamengine and icd. Adjudicated value: Inactive. Lesson: the codebook should say explicitly that the default branch is the reference, and should carry a current reference date.

## Example 3 — libnegf_libnegf (WhyRecovered)
**Project owner:** Benjamin Noyes (bnoyes). **Validator:** Casey Collins (ccolli78).
**Author:** "The project had a period of inactivity but started getting updates again when more bugs needed fixing."
**Validator:** "Maintainer (Alessandro Pecchia) merged two pending PRs, a README fix and Daniele Soccodato's quasi-equilibrium density feature. Bug fixes to the API and real-axis integration followed six months later."
**Evidence:** The first post-gap commits (2023-05-31) are "Merge pull request #66 Update README.md" and "Merge pull request #69 from DanSoccodato/quasiEq-density". The bug-fix commits ("Solved a bug in libnegf API", "Fixed real_axis_int for electrons", "Fixed allocation problems") come in 2023-11 and 2023-12.
**Discussion:** Benjamin's answer was not wrong, the bug fixes did happen, but they are the second wave of activity rather than the trigger. The gap actually ended when the maintainer cleared a backlog of contributor pull requests. We merged the two readings.
**Resolution:** Compromise. Adjudicated value: "Maintainer merged two pending contributor PRs (README fix and quasi-equilibrium density feature) in May 2023. Bug fixes to the API and real-axis integration followed six months later." The two other WhyRecovered disagreements (helske_kfas, badlands-model_badlands) had the same shape: a generic reason ("fixes and updates", "older code needed work") versus the specific trigger visible in the commit messages.

## Example 4 — philipperemy_keras-tcn (RecentThemes)
**Project owner:** Benjamin Noyes (bnoyes). **Validator:** Casey Collins (ccolli78).
**Author:** Dependency updates:Release
**Validator:** Bug fixes:Release
**Evidence:** Benjamin's data was pulled in 2025-03/04, when the latest ten commits were TensorFlow 2.19 support, the removal of tensorflow-addons and a version bump. Casey validated against GitHub in 2026-10, when the latest ten included "fix lr, to work with both old & new keras (#284)" and two "Update tcn.py" fixes.
**Discussion:** Both values were correct for the commits each of us was looking at. The disagreement is snapshot drift, not interpretation. We agreed to grade RecentThemes against the author's data snapshot, and applied the same rule to spacetelescope_mirage (AuthorKept) and badlands-model_badlands (Compromise, since neither original value fit Benjamin's own snapshot, which was dominated by environment.yml dependency edits).
**Resolution:** AuthorKept. Adjudicated value: Dependency updates:Release. Lesson: validation of "recent" fields must fix a reference date, otherwise author and validator are coding different commits.
