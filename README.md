# Truck Disposal Detection – Bosch Camera Configuration

This repository contains **Bosch IVA (Intelligent Video Analytics)** configuration scripts used to detect trucks that **leave the unloading area (tolva) without disposing of their soybeans**.
---

## ⚙️ Overview

These scripts define the logic inside a Bosch IVA camera to automatically trigger alerts when:

1. A **truck enters** the tolva area (`Entrada` task).  
2. The truck **is detected unloading** inside the tolva (`Tolva` task).  
3. The truck **exits** the tolva (`Salida` task).  
4. The system checks whether the truck **unloaded before exiting**.  
   - If **no unloading event** occurred → an **email alert** is automatically sent.

---

## ✉️ Email Notification Setup

The file `IVAAlarmTaskEditor` defines how the camera sends email alerts.

To enable email notifications:

1. Open your **Bosch Configuration Manager** or **VCA Task Editor**.  
2. In the **Alarm Task Editor** section, copy and paste the content of  
   `IVAAlarmTaskEditor`.
3. Replace the placeholder values:
IP("smtp.example.com")
From("camera@example.com")
Login("camera@example.com")
Password("APP_PASSWORD")
To("alerts@example.com")

4. Make sure that the sender email account supports **SMTP** (not POP3 or IMAP).
- **SMTP (Simple Mail Transfer Protocol)** is required to **send** emails.
- If your provider uses **two-factor authentication**, create an **app-specific password**.
5. Test the configuration by triggering a manual alert from the camera interface.

> ⚠️ **Do not use POP3 or IMAP** — these are protocols for **receiving** email, not sending.  
> The camera must be configured with an **SMTP sender account** to send notifications automatically.

---

## 🧠 Camera Rule Summary

| Task Name | Description |
|------------|--------------|
| **Entrada** | Detects truck crossing the entrance line into the tolva zone. |
| **Tolva** | Detects truck presence inside the unloading area. |
| **Salida** | Detects truck exiting the tolva area. |
| **Salida después de descarga** | Confirms if the truck exited **after unloading**. If not, triggers an email alert. |

---

## ⚠️ Security & Best Practices

- **Never commit real credentials** to GitHub.  
- Use placeholders (`example.com`, `APP_PASSWORD`) in configuration files.  
- Keep your SMTP credentials configured **only on the camera**.  
- Ensure your email account supports **TLS/STARTTLS** for secure transmission.

---

## 🧰 How to Import

1. Open Bosch **IVA Task Editor**.
2. Import or copy/paste:
- `BoschIvaTaskEditor` → under the **IVA Tasks** section.
- `IVAAlarmTaskEditor` → under **Alarm Task Editor**.
3. Adjust geometric coordinates (`Field`, `Line`) according to your camera’s position.
4. Apply and save configuration to the camera.

---

## 📝 License

MIT License – free to use and modify.  
Attribution appreciated but not required.
