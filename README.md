![AWS Log](./aws.webp)

# AWS Projects — Flask Hands‑ons & CloudFront Kittens

This README describes four small, focused learning projects that live under the **AWS Projects** folder. It clarifies what each project is, which AWS services or Flask topics it covers, what files are expected, and how to verify success. It is intentionally free of code snippets so it can serve as a clean, high‑level guide.

1. **Hands‑on Flask‑01‑02:** First Flask app, “Hello, World!”, and basic Jinja templates
2. **Hands‑on Flask‑03‑04:** Jinja `if`/`for`, routing patterns, and handling GET/POST
3. **Hands‑on Flask‑05:** Using SQL with a Flask web app (SQLAlchemy‑based)
4. **Project‑006:** Kittens Carousel static website on S3 + CloudFront + Route 53 (provisioned with CloudFormation)

---

## Table of Contents

- Prerequisites
- Recommended Folder Structure
- Project Summaries

  - Flask‑01‑02
  - Flask‑03‑04
  - Flask‑05
  - Project‑006 (S3 + CloudFront + Route 53)

- Conventional Commits (suggested)
- Troubleshooting
- License

---

## Prerequisites

- Python 3.10 or newer
- pip
- Git
- AWS account with permissions for S3, CloudFront, Route 53, and CloudFormation
- (Optional) AWS CLI v2 configured for deployments
- (Optional) Virtual environments (venv) for Python isolation

---

## Recommended Folder Structure

- **AWS Projects**

  - **Flask‑01‑02‑Hello‑Jinja**

    - `app.py`, `requirements.txt`, `templates/` (e.g., `base.html`, `index.html`)

  - **Flask‑03‑04‑Routes‑Forms**

    - `app.py`, `requirements.txt`, `templates/` (e.g., list and form views)

  - **Flask‑05‑SQLAlchemy**

    - `app.py`, `models.py`, `requirements.txt`, `templates/` (e.g., listing page)

  - **Project‑006‑Kittens‑Carousel‑CFN**

    - `site/` (static assets and `index.html`)
    - `cloudformation/` (infrastructure templates)

File names are suggestions; keep a consistent naming scheme across projects.

---

## Project Summaries

### Hands‑on Flask‑01‑02

**Title:** Creating First Flask Application — Hello World and basic Jinja templates

**Goals**

- Spin up a minimal Flask application
- Practice Jinja basics: template inheritance and variable rendering

**Key Topics**

- Flask application structure
- `templates/` directory conventions
- Rendering values into HTML

**Deliverables**

- Application file and two templates (`base.html`, `index.html`)

**Validation Checklist**

- Root route returns HTTP 200
- Title and name render correctly via Jinja

---

### Hands‑on Flask‑03‑04

**Title:** If‑For structure, Routing, and GET/POST methods

**Goals**

- Use Jinja `if`/`for` for conditional lists and empty states
- Create dynamic routes with path parameters
- Handle simple forms with GET (filter/search) and POST (create)

**Key Topics**

- Request handling and route decorators
- Passing data to templates
- Redirects after POST

**Deliverables**

- Application file and templates for listing and form pages

**Validation Checklist**

- GET query parameter filters the list
- Submitting a POST adds an item and returns to the list view

---

### Hands‑on Flask‑05

**Title:** Handling SQL with a Flask Web Application

**Goals**

- Configure SQLAlchemy for a small Flask app
- Create a model and implement basic CRUD operations

**Key Topics**

- Database URI and application context
- Creating tables and persisting records
- Rendering database records in templates

**Deliverables**

- `app.py`, `models.py`, and a template to list/add records

**Validation Checklist**

- Local database file is created on first run (e.g., SQLite)
- Records persist across application restarts

---

### Project‑006: Kittens Carousel (S3 + CloudFront + Route 53 via CloudFormation)

**Title:** Static website deployment using CloudFront, S3, and Route 53 (Infrastructure as Code)

**Goals**

- Host a static site in S3
- Serve content securely and efficiently through CloudFront
- Map a custom domain using Route 53
- Provision the entire stack with CloudFormation

**Architecture at a glance**

- **Amazon S3**: stores static assets (HTML, CSS, images)
- **Amazon CloudFront**: global CDN in front of S3 for performance and HTTPS
- **AWS CloudFormation**: reproducible provisioning of bucket, distribution, and DNS
- **Amazon Route 53**: DNS record pointing the chosen domain/subdomain to CloudFront

**Inputs (typical)**

- Root domain (e.g., `example.com`)
- Subdomain (e.g., `www`)
- Hosted Zone ID for the domain
- (Optional) ACM certificate in `us‑east‑1` for a custom TLS certificate

**Deployment Outline**

1. Ensure a Route 53 hosted zone exists for your domain.
2. (Optional) Request or validate an ACM certificate in `us‑east‑1` for the domain.
3. Deploy the CloudFormation template to create S3, CloudFront, and DNS records.
4. Upload the `site/` contents to the provisioned S3 bucket.
5. Confirm that the website loads via the CloudFront domain and your custom domain.

**Security Notes**

- Public access to the S3 bucket should remain blocked; CloudFront is the public entry point.
- Use Origin Access Control (or OAI) so only CloudFront can read the bucket contents.

**Acceptance Criteria**

- CloudFormation stack finishes successfully
- `index.html` is reachable through CloudFront and your domain
- Direct S3 object access is blocked when expected

---

## Conventional Commits (suggested)

- `feat(flask-03-04): add POST add-item flow`
- `fix(flask-05): persist color field in list view`
- `docs(project-006): add high-level deploy outline`
- `chore: bump Flask version`

---

## Troubleshooting

**Flask won’t start**

- Wrong working directory or missing dependencies
- Port conflict; change the port and retry

**Templates not found**

- `templates/` directory must be alongside the application file
- If you use a different folder name, configure it explicitly at app creation

**CloudFormation fails**

- Hosted Zone must match the target domain
- Custom TLS certificates for CloudFront live in `us‑east‑1`
- S3 bucket names are globally unique; pick an unused name

**Blocked object access**

- Expected when using OAC/OAI. Always access content via CloudFront or your domain.

---

## License

Learning exercises. Use freely within your portfolio and projects.
