# 📘 CPTSC 2025 Structured Authoring Workshop Template

Template repository for publishing **Bootstrap-themed HTML** and **PDF** outputs using [DITA-OT build GitHub Action](https://github.com/dita-ot/dita-ot-action). Use this guide to upload a DITA project to a GitHub repository and, via DITA-OT GitHub Actions, access website and pdf deliverables. Edits to DITA files committed to the repository will invoke the DITA-OT automatically in a process of continuous integration and development to build and serve website and pdf deliverables.

---

## 🧭 Table of Contents

- [🧩 Prerequisite](#-prerequisite)
- [🚀 Getting Started](#-getting-started)
- [🔑 Grant Workflow Permissions](#-grant-workflow-permissions)
- [🧱 Project Layout & Requirements](#-project-layout--requirements)
- [⚙️ Build & Publish (CI Workflow)](#️-build--publish-ci-workflow)
- [🌐 Enable & View GitHub Pages](#-enable--view-github-pages)
- [🎨 Customize the Outputs](#-customize-the-outputs)
  - [🖼️ PDF Theme](#️-pdf-theme)
  - [🖥️ Website Theme](#️-website-theme)
- [🛟 Troubleshooting](#-troubleshooting)
- [🙌 Credits](#-credits)

---

## 🧩 Prerequisite

You must be logged in to your personal account on GitHub to use this template (refer to [Creating an account on GitHub](https://docs.github.com/en/get-started/start-your-journey/creating-an-account-on-github) for instructions). 

---

## 🚀 Getting Started

1. Click **“Use this template”** at the top of this page.  
2. Create your new repository from the template.  
   - ✅ **Select “Include all branches.”** You’ll need all branches provided by the template.


## 🔑 Grant Workflow Permissions

Give the built-in `GITHUB_TOKEN` permission to publish:

1. **Settings → Actions → General**  
2. Under **Workflow permissions**, select **Read and write permissions**  
3. (Optional but recommended) Check **Allow GitHub Actions to create and approve pull requests**

> 📝 Without write permissions, the workflow cannot push to the `gh-pages` branch for GitHub Pages.

---

## 🧱 Project Layout & Requirements

Put all of your DITA content inside the `dita` directory:

```repo-root/
├─ .github/
│ ├─ workflows/
│ │ └─ ci.yml
│ ├─ dita-ot/
│ │ ├─ header.xml
│ │ ├─ footer.xml
│ │ └─ theme.css
│ └─ themes/
│ ├─ logo.png
│ └─ theme.yaml
└─ dita/
│├─ document.ditamap ← main map (required by the default workflow)
│├─ index.dita ← homepage topic for the site
│├─ topics/…
│└─ images/…
```

**Requirements**

- 📄 **Main map name**: The default workflow expects **`document.ditamap`**.  
  - Rename your DITA map **`document.ditamap`**.
  - You *can* give it different name, but then you must update the workflow where it references `document.ditamap` (open `.github/workflows/ci.yml` and search for that filename).
- 🏠 **Homepage**: `dita/index.dita` will serve as the site’s landing page.
  - Create an index.dita generic or concept topic. Suggest doing this before putting your DITA content inside the dita directory. 
  - Reference your `index.dita` as the first topic reference in your `document.ditamap`. Otherwise, your deliverables will not have a home page or introduction. Suggest doing this before putting your DITA content inside the dita directory. The index.dita topic might include overview or about information.
- 📁 Keep topics, maps, and media under the `dita/` folder.

---

## ⚙️ Build & Publish (CI Workflow)

- Every **push** to the repository triggers the build defined in **`.github/workflows/ci.yml`**.  
- The workflow runs DITA-OT to generate:
  - 🌐 **[Bootstrap](https://getbootstrap.com/)-themed HTML**
  - 📄 **PDF**

## 🌐 Enable & View GitHub Pages

1. **Settings → Pages**  
2. **Source**: select **Deploy from a branch**  
3. **Branch**: choose **`gh-pages`** and **`/ (root)`**, then **Save**  
4. Your site will be available at:  
`https://<your-username>.github.io/<your-repo>/`

## 📊 Monitor Workflow Runs

- Go to the **Actions** tab → open the most recent run.
- ✅ **Green check** = success | ❌ **Red X** = failed  
- Click into a failed job to read logs. Typical causes:
  - Missing `document.ditamap` or broken references
  - Invalid DITA markup
  - Insufficient token permissions to push to `gh-pages`

> ⏱️ Builds and page deployments can take a few minute to appear after a successful run.

## 📄 PDF Deliverable

The PDF output is not deployed directly to GitHub Pages.  
Instead, each workflow run on the **Actions** page provides the PDF as a downloadable **artifact**:

1. Go to the **Actions** tab in your repository.  
2. Select the latest successful workflow run.  
3. Scroll down to the **Artifacts** section.  
4. Click the PDF artifact link to download your deliverable. 

---

## 🎨 Customize the Outputs

### 🖼️ PDF Theme

- Replace the logo at **`.github/themes/logo.jpg`** with your own.  
- Keep the **filename as `logo.jpg`** unless you also update the workflow.  
- Edit **`.github/themes/theme.yaml`** to adjust **brand colors, fonts, and layout**.  
- 💡 Not comfortable with YAML? Paste the file into an LLM and request guided edits.

### 🖥️ Website Theme

- Update the header text in **`.github/dita-ot/header.xml`** (default shown below):

`<span class="align-middle">DITA Open Toolkit experiments</span>`

- Modify `.github/dita-ot/footer.xml` as needed.
- Adjust `.github/dita-ot/theme.css` to change colors, fonts, and layout.
- 💡 Not comfortable with CSS? Paste it into an LLM and ask for brand-aligned changes.

For advanced options and components, see the [`dita-bootstrap` plugin documentation](https://infotexture.github.io/dita-bootstrap/).

## 🛟 Troubleshooting
- No site/404 on Pages
  - Confirm Settings → Pages is set to `gh-pages / root`.
  - Check that the CI run completed successfully and pushed to gh-pages.
- Workflow cannot push
 -Verify Read and write permissions for GITHUB_TOKEN (see above).
- Build fails with missing files
  - Ensure `dita/document.ditamap` exists and references are correct.

## 🙌 Credits

Thanks to the following DITA-OT experts and maintainers:
- Jason Fox
- Roger Sheen
