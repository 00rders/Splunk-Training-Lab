# 🟢 Splunk Cloud Training Lab&#x20;

**Cloud-ready lab to learn Splunk search, detection, dashboarding, and alert triage — built by a self-taught analyst → for self-taught analysts.**

---

## 📌 About

This repo provides a **realistic, self-paced environment** to build Splunk skills aligned with the **Splunk Core Certified User** and **Power User** certifications.

All exercises are fully compatible with **Splunk Cloud Free Trial**, so you can train without needing to install Splunk locally.

---

## 💻 1. Prerequisites

* 🚀 **Splunk Cloud Trial Account** → [Sign up here](https://www.splunk.com/en_us/cloud-trial.html)
* 🔗 Access Splunk via browser: `https://<yoursubdomain>.splunkcloud.com`
* 📒 Download the contents of this repo or clone it locally

---

## 📁 2. Folder Structure

```bash
splunk-training-lab/
├── sample-data/        # Log files to upload into Splunk Cloud
│   └── web_access.log
├── saved-searches/     # SPL queries for practice
│   └── search-examples.txt
├── dashboards/         # Pre-built dashboard XML
│   └── sample-dashboard.xml
├── lookups/            # CSV lookup tables
│   └── users.csv
└── README.md           # This guide
```

---

## 📂 3. Upload Sample Data to Splunk Cloud

1. In Splunk Cloud: **Settings > Add Data**
2. Select **Upload** and choose `sample-data/web_access.log`
3. Set sourcetype to `apache_logs` (or define a new one)
4. Choose or create an index (e.g., `practice_index`)
5. Complete the wizard and start searching

---

## 🔍 4. SPL Practice Queries

Open `saved-searches/search-examples.txt` and paste into the Splunk Search bar.

```spl
# View all logs\index=practice_index

# Filter by status code
index=practice_index status=200

# Last hour of logs
index=practice_index earliest=-1h@h latest=now

# Extract endpoint using regex
index=practice_index | rex "GET\\s(?<endpoint>/\\S+)\\sHTTP"

# Display in table
index=practice_index | table _time, clientip, endpoint, status
```

---

## 📊 5. Build Dashboards in Splunk Cloud

1. Go to **Dashboards > Create New Dashboard**
2. Copy/paste contents of `dashboards/sample-dashboard.xml` (optional)

```xml
<dashboard>
  <label>Web Traffic Overview</label>
  <row>
    <panel>
      <chart>
        <title>Requests per Hour</title>
        <search>
          <query>index=practice_index | timechart count by status</query>
        </search>
      </chart>
    </panel>
  </row>
</dashboard>
```

---

## 🔄 6. Use Lookups

1. In Splunk Cloud: **Settings > Lookups > Lookup Table Files**
2. Upload `lookups/users.csv`

**CSV Example:**

```csv
ip_address,username
192.168.1.5,john_doe
10.0.0.1,jane_admin
```

**Search with lookup:**

```spl
index=practice_index | lookup users.csv ip_address AS clientip OUTPUT username
```

---

## 🧪 7. Go Further

* Create field extractions: **Settings > Fields > Field Extractions**
* Set alerts (e.g. 5xx error spikes, login failures)
* Upload other logs (syslog, firewall, JSON)
* Build and share your own dashboards or challenges

---

## 📘 Resources

* [Splunk SPL Reference](https://docs.splunk.com/Documentation/Splunk/latest/SearchReference/Whatsinthismanual)
* [Splunk Cloud Docs](https://docs.splunk.com/Documentation/SplunkCloud)
* [Splunk Core User Exam Guide](https://www.splunk.com/en_us/training/certification-track/splunk-core-certified-user.html)

---

## 🤝 Contribute

Got ideas, dashboards, or new data sources? Fork this repo and submit a PR.

---

## 🔐 License

[MIT License](LICENSE) — free to use, adapt, and expand.

---

> Built by an aspiring Splunk professional > for aspiring Splunk professionals
