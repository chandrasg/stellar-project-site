# STELLAR Project Website

**Steering-Vector Enhanced LLM Agents for Realistic Digital Twins in Mental Health**

A Wellcome Trust-funded collaboration between NYU, University of Pennsylvania, and the Linguistic Data Consortium.

## Live site

Once deployed, the site will be available at:
`https://<your-github-username>.github.io/stellar-project-site/`

## Deployment

This is a single-page static site — no build step required. It runs directly on GitHub Pages.

### Setup

1. Push this repo to GitHub
2. Go to **Settings → Pages**
3. Under "Source", select **Deploy from a branch**
4. Choose `main` branch, root `/`
5. Save — the site will be live in ~1 minute

### Custom domain (optional)

To use a custom domain (e.g., `stellar-project.org`):

1. Add a `CNAME` file containing just the domain name
2. Configure DNS with your registrar (CNAME → `<username>.github.io`)
3. Enable HTTPS in GitHub Pages settings

## Editing

The entire site is in `index.html`. Key sections to update:

- **Team**: Search for `team-grid` — each person is a `team-card` div
- **Publications**: Search for `pub-list` — each paper is a `pub-item` div
- **Open positions**: Search for `position-cards` — each role is a `position-card` div
- **Google Form link**: Search for `forms.gle/PLACEHOLDER` and replace with your actual form URL

## TODO

- [ ] Replace `https://forms.gle/PLACEHOLDER` with actual Google Form URL
- [ ] Confirm team bios with all investigators
- [ ] Add team photos (optional — would require adding `<img>` tags to team cards)
- [ ] Add Wellcome Trust logo if permitted
- [ ] Set up custom domain if desired

## License

Content © 2026 STELLAR Project. All rights reserved.
