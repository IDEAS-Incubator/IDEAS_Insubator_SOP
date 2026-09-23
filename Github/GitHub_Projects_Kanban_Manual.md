# GitHub Projects: Kanban Board Manual

GitHub Projects is a planning tool built on top of your issues and pull requests. A Kanban board is one *view* of a project: cards sit in columns by status and move left to right as work progresses. This guide covers the current version of Projects. The old "Projects (classic)" has been retired.

---

## 1. Core concepts

**Project.** A project lives at the user or organization level, not inside one repo, so a single board can track work across many repositories. You can link a project to specific repos so it appears in their Projects tab.

**Items.** A card on the board is one of three things:

- an **issue**
- a **pull request**
- a **draft issue**, which is a quick note that exists only in the project until you convert it into a real issue

**Fields.** Every item has fields. The board's columns come from a single-select field, usually the built-in **Status**. You can also add custom fields such as Priority, Size, Estimate, dates, or Iteration (sprints).

**Views.** The same data can be shown as a **Board** (Kanban), a **Table** (spreadsheet), or a **Roadmap** (timeline). Each view has its own filters, grouping, and sorting.

---

## 2. Create a Kanban project

1. Go to your profile, or your organization page, and open the **Projects** tab.
2. Click **New project**.
3. Pick the **Kanban** template. It comes with Todo / In Progress / Done columns and useful automations. Alternatively, choose **Board** under "Start from scratch."
4. Name the project and click **Create project**.
5. Optional: link it to a repository. Open the repo, go to the **Projects** tab, click **Link a project**, and select it.

---

## 3. Set up your columns

The columns are the options of the **Status** field.

- **Add a column:** click **+** at the far right of the board and name the new status.
- **Rename, reorder, or delete a column:** use the **⋯** menu on the column header. You can also edit the Status field's options under project **Settings → Fields → Status**.
- **Set a WIP limit:** open the column **⋯** menu, choose **Set limit**, and enter a number. The count turns red when the column exceeds the limit. This is the heart of real Kanban practice.
- **Add a description:** also in the column menu. It's a good place to state the "definition of done" for that stage.

A column setup that works well for most teams:

**Backlog → Ready → In progress → In review → Done**

---

## 4. Add items to the board

**From the board:** click **+ Add item** at the bottom of a column, then do one of the following:

- Type a title and press Enter to create a **draft issue**.
- Type `#`, pick a repository, then pick an existing issue or PR.
- Paste the URL of an issue or PR.

**From a repository:** in the repo's Issues list, select several issues with the checkboxes, click **Projects**, and choose your project to add them in bulk.

**From an issue or PR page:** in the right sidebar, click **Projects** and select the project.

**Convert a draft into a real issue:** open the draft card, click **Convert to issue**, and choose a repo.

---

## 5. Work with cards

- **Move a card:** drag it to another column. This updates its Status.
- **Open a card:** click it to open a side panel where you can edit fields, assignees, labels, and milestone, and read or comment on the issue without leaving the board.
- **Reorder cards within a column:** drag up or down to set priority.
- **Archive finished cards:** use the card's **⋯** menu and choose **Archive**. Archived items are hidden but recoverable from **⋯ → Archived items**.

---

## 6. Add custom fields

Go to **Settings → Fields → + New field**, or click **+** on the header row of a table view. Field types include:

| Type | Example use |
|---|---|
| Single select | Priority (P0/P1/P2), Size (S/M/L), Team |
| Text | Notes, owner email |
| Number | Story points, estimate hours |
| Date | Due date, start date |
| Iteration | 2-week sprints with automatic start/end dates |

To show field values on cards, open the **view menu (▾ next to the view name)**, choose **Fields**, and toggle the fields you want visible.

---

## 7. Customize the board view

Open the **▾** menu next to the view tab name to find these settings:

- **Column by:** choose which single-select or iteration field defines the columns. For example, switch from Status to Iteration to get a sprint board.
- **Group by:** creates horizontal **swimlanes**, such as one lane per assignee, priority, or repo.
- **Sort by:** order cards within columns.
- **Field sum:** shows the total of a number field per column, such as total story points in "In progress."
- **Duplicate view / New view:** create several saved views, such as "My work," "Bugs only," or "Current sprint."

Changes are unsaved until you click **Save** (the view tab shows a dot when it has unsaved edits).

### Filter syntax

Type into the filter bar at the top of a view:

```
assignee:@me                  my items
status:"In progress"          one column
-status:Done                  exclude done
label:bug priority:P0         combine conditions (AND)
label:bug,enhancement         either label (OR)
is:issue is:open              only open issues
iteration:@current            current sprint
repo:owner/repo-name          one repository
no:assignee                   unassigned items
```

---

## 8. Automate with workflows

Open **⋯ (top right) → Workflows**. The built-in workflows include:

| Workflow | What it does |
|---|---|
| Item added to project | Sets Status (e.g. to *Backlog*) automatically |
| Item closed | Moves the card to *Done* |
| Pull request merged | Moves the card to *Done* |
| Item reopened | Moves the card back to *In progress* |
| Auto-archive items | Archives items matching a filter, e.g. `is:closed updated:<@today-2w` |
| Auto-add to project | Adds new issues/PRs from a repo that match a filter, e.g. `is:issue label:bug` |

Toggle a workflow on, edit its target value, and save.

**Tip:** write `Closes #42` in a PR description. When the PR merges, issue #42 closes and the "Item closed" workflow moves its card to Done automatically.

For more advanced automation, use **GitHub Actions** together with the **Projects GraphQL API**. For example, you can set a field whenever a label is added.

---

## 9. Track progress with Insights

Click **Insights** (the chart icon at the top). The default burn-up chart shows completed versus open items over time. You can create new charts, such as a bar chart of items per Status grouped by assignee, to spot bottlenecks.

---

## 10. Access and sharing

Under **⋯ → Settings**:

- **Visibility:** Public or Private.
- **Manage access:** invite collaborators or teams with Read, Write, or Admin roles.
- **README and short description:** explain the board's purpose and column rules for newcomers.
- **Make a template (org projects):** save your board setup so teams can reuse it.

Note that a user can see an issue on the board only if they also have access to its repository.

---

## 11. Best practices

1. **Keep WIP limits low.** Finishing work beats starting work.
2. **Pull, don't push.** People take cards from *Ready* when they have capacity.
3. **One card = one deliverable.** Split anything bigger than a few days of work, using sub-issues if needed.
4. **Let automation move cards to Done.** Closing an issue or merging a PR should update the board on its own.
5. **Make personal views.** For example, an `assignee:@me -status:Done` view gives each person a focused board.
6. **Review weekly.** Groom the Backlog, check Insights, and archive old items.

---

## Quick keyboard shortcuts

| Key | Action |
|---|---|
| `Ctrl/Cmd + K` | Command palette |
| `Ctrl/Cmd + F` | Focus filter bar |
| `Enter` | Open selected card |
| `Space` | Select card |
| Arrow keys | Move selection |
