# Legal Guide

<licensing>
## Choosing a License

| License | Use when | Allows | Requires |
|---------|----------|--------|----------|
| **MIT** | Libraries, tools, most projects | Commercial use, modification, distribution | License notice |
| **Apache 2.0** | Larger projects, patent protection needed | Same as MIT + patent grant | License notice, state changes |
| **GPL 3.0** | Want derivatives to stay open source | Same as above | Derivatives must be GPL |
| **ISC** | Minimal, BSD-like | Same as MIT | License notice |
| **Unlicense** | Public domain dedication | Everything | Nothing |
| **Proprietary** | Closed source commercial | Nothing (default) | N/A |

**Default recommendation:** MIT for most projects.

## LICENSE File

Create `LICENSE` file in project root:

```
MIT License

Copyright (c) [year] [fullname]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## Third-Party Licenses

**Before adding a dependency, check license compatibility:**

| Your License | Can use MIT? | Can use Apache? | Can use GPL? |
|--------------|--------------|-----------------|--------------|
| MIT | Yes | Yes | No (viral) |
| Apache 2.0 | Yes | Yes | No (viral) |
| GPL | Yes | Yes | Yes |
| Proprietary | Yes | Yes | No |

**GPL is "viral"** - if you use GPL code, your entire project must be GPL.
</licensing>

<privacy>
## GDPR/DSGVO Compliance (EU/DE)

**Core principles:**
1. **Data minimization** - Collect only what's necessary
2. **Purpose limitation** - Use data only for stated purpose
3. **Consent required** - Get explicit consent before collecting
4. **Right to deletion** - Users can request data deletion
5. **Transparency** - Tell users what you collect and why

**Required for user-facing apps:**
- Privacy Policy (Datenschutzerklaerung)
- Cookie consent banner (if using cookies/tracking)
- Data processing documentation
- Contact for privacy requests

**Privacy Policy must include:**
- What data is collected
- Why it's collected (purpose)
- How long it's stored
- Who has access (third parties)
- User rights (access, deletion, etc.)
- Contact information

**Do NOT:**
- Track users without consent
- Share data with third parties without disclosure
- Store data longer than necessary
- Collect data "just in case"
</privacy>

<impressum>
## Impressum (German Law - TMG/DDG)

**Required for:** All commercial/business websites accessible from Germany.

**Must contain:**
1. Full legal name (person or company)
2. Physical address (no PO boxes)
3. Contact: Email AND phone/fax
4. VAT ID (USt-IdNr.) if applicable
5. Trade register info if applicable
6. Responsible for content (V.i.S.d.P.)

**Example:**
```
Impressum

Max Mustermann
Musterstrasse 123
12345 Musterstadt
Deutschland

E-Mail: kontakt@example.de
Telefon: +49 123 456789

USt-IdNr.: DE123456789

Verantwortlich fuer den Inhalt nach DDG:
Max Mustermann (Anschrift wie oben)
```

**Placement:**
- Must be easily accessible (max 2 clicks from any page)
- Usually in footer: "Impressum" link
- Can be combined with "Legal" or "About" page

**Exceptions:**
- Purely private, non-commercial websites
- But: Having ads = commercial = Impressum required
</impressum>

<checklist>
## Legal Checklist for New Projects

**Before launch:**
- [ ] LICENSE file in root
- [ ] Third-party licenses compatible
- [ ] Privacy Policy (if collecting user data)
- [ ] Cookie consent (if using cookies/tracking)
- [ ] Impressum (if accessible from DE + commercial)

**Ongoing:**
- [ ] Update Privacy Policy when data practices change
- [ ] Document data processing activities
- [ ] Handle deletion requests within 30 days
</checklist>
