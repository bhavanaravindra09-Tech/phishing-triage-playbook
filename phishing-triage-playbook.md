# Phishing Triage Playbook

One-page incident response for a **reported suspicious email**.
Keep it to one page — in the moment, nobody reads a manual.

## 1. IDENTIFY (first 15 minutes)

- [ ] Confirm the report: sender address, subject, timestamp, recipients.
- [ ] Ask the reporter: **did you click a link, open an attachment, or enter
      credentials?** (This single answer sets the severity.)
- [ ] Do NOT click links or open attachments yourself — inspect headers and
      URLs by hovering.
- [ ] Search the mail system for the same sender/subject → list **all**
      recipients, including anyone who hasn't reported.

**Notify:** your direct lead / SOC channel. **Log:** reporter, sender,
subject, recipient count, click/no-click status.

## 2. CONTAIN

- [ ] If **no click**: user deletes the message; check for malicious inbox
      rules (Outlook → Rules — attackers hide replies there); done.
- [ ] If **credentials entered**: reset the password immediately, revoke all
      active sessions/tokens, verify MFA is on.
- [ ] If **attachment opened**: isolate the machine from the network
      (unplug/disable Wi-Fi) — do NOT power it off; escalate to security.
- [ ] Pull the message from other recipients' mailboxes (admin quarantine /
      delete) so nobody else clicks.
- [ ] Block the sender domain/URLs at the mail gateway if the tooling allows.

**Notify:** security team if credentials were entered or malware ran.
**Log:** containment actions + timestamps.

## 3. ERADICATE

- [ ] Confirm the phishing message is removed from every mailbox.
- [ ] If a machine was isolated: hand it to security for imaging/forensics —
      do not "clean and return" a potentially compromised host on your own.
- [ ] Remove any persistence found (inbox rules, forwarding addresses,
      unknown OAuth app consents).

**Log:** eradication steps and who performed them.

## 4. RECOVER

- [ ] Restore the user to normal operation (new password set, sessions fresh,
      mailbox rules clean).
- [ ] Monitor the affected account for 7 days (impossible-travel logins,
      new forwarding rules, mass deletions).
- [ ] Close the ticket only after the monitoring window, not after the
      password reset.

## 5. LESSONS LEARNED (within 48h)

- [ ] 15-minute debrief: how did it get past filters? What worked in the
      response? What was slow?
- [ ] If multiple people received it: send a short all-clear + reminder
      ("thanks to X for reporting fast — here's what to watch for").
- [ ] Update this playbook with anything you learned.

---

**Escalate immediately (don't wait for the phases) if:** credentials for a
privileged/admin account were entered · an internal account is sending the
phish (possible account takeover) · ransomware-like behaviour appears.
