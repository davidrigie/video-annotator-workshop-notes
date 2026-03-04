# Build Log
*Chronological log of steps taken while building the app*

---

## 2026-03-03

1. Used Glean to search for a JIRA issue related to procedure recordings. Found relevant issue and downloaded the procedure recording files to the project directory.
2. Gave Claude the opening prompt describing the app idea — a video annotation tool for reviewing long procedure recordings (30-60 min) to find and annotate specific frames related to bugs/complaints. Key requirements laid out:
   - Load and scrub through video files
   - Annotate specific portions of frames with comments
   - View all timestamped annotations for a video
   - Share findings with others
   - Export standalone reports with screenshots + comments for uploading to JIRA
   - Asked Claude to create a `CLAUDE.md` and tailor its approach for a non-coder
3. Reviewed the generated `CLAUDE.md`, gave feedback on something that wasn't right.
4. Asked Claude to make the `CLAUDE.md` more concise to save context window space.
5. Corrected Claude again — it assumed web app, but it doesn't need to be a web app.
6. Told Claude not to include app-specific details in `CLAUDE.md` yet — a detailed plan will come next as a separate step.
7. Asked Claude to create a detailed plan, triggering it to enter plan mode. Told it to write the plan file to the project folder (by default it writes to a centralized location).
8. Asked Claude to update its own instructions to use git for version control automatically and hide the details — phrased simply: *"Update your instructions to use git for version control, but do it automatically and hide the details from me since I'm not familiar with git."* Claude generated the `CLAUDE.md` version control section on its own.
9. First version of the app ran — looked cool but had a lot of issues.
10. Started testing the app and reporting issues to Claude — describing clearly what isn't working as intended.
11. Asked Claude to enter plan mode again to address the accumulated issues plus a design change (switching from web app to local/desktop app).
12. Claude suggested commands to run for testing — instead of running them manually, just asked Claude to do it.
13. After switching to local app, hit a video loading issue. Claude has tried multiple fixes but hasn't resolved it yet — stuck in a loop. Suspecting the mid-development pivot from web app to local app left behind residual issues — would have likely been smoother if it started as a local app from the beginning.
14. After a few more iterations of feedback and fixes, got to a very useful and usable app.
15. Shifted focus to refining the user experience — polishing UI and usability details.
16. UI tweaks broke some core features — be careful with cosmetic changes breaking functionality.
17. Got to a nice stable state — asked Claude to "tag" the version in git as a save point.
