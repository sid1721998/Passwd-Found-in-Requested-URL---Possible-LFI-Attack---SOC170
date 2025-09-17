# Passwd-Found-in-Requested-URL---Possible-LFI-Attack---SOC170
Passwd Found in Requested URL - Possible LFI Attack - SOC170
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SOC Incident Report – SOC170</title>
<style>
  body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    margin: 20px;
    background-color: #f5f7fa;
    color: #333;
  }
  h1, h2, h3 {
    color: #222;
  }
  h1 {
    text-align: center;
    margin-bottom: 10px;
  }
  .severity-high {
    color: #fff;
    background-color: #e74c3c;
    display: inline-block;
    padding: 2px 8px;
    border-radius: 4px;
    font-weight: bold;
  }
  table {
    width: 100%;
    border-collapse: collapse;
    margin-bottom: 20px;
    background-color: #fff;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
  }
  th, td {
    border: 1px solid #ddd;
    padding: 10px;
    text-align: left;
  }
  th {
    background-color: #3498db;
    color: #fff;
  }
  tr:nth-child(even) {
    background-color: #f2f6f8;
  }
  tr:hover {
    background-color: #e1f0ff;
  }
  .section {
    margin-bottom: 30px;
  }
  .legend span {
    display: inline-block;
    width: 15px;
    height: 15px;
    margin-right: 5px;
    vertical-align: middle;
    border-radius: 3px;
  }
  .legend .high { background-color: #e74c3c; }
  .legend .medium { background-color: #f1c40f; }
  .legend .low { background-color: #2ecc71; }
  pre {
    background-color: #ecf0f1;
    padding: 10px;
    border-radius: 4px;
    overflow-x: auto;
  }
</style>
</head>
<body>

<h1>SOC Incident Report</h1>
<h2>Incident ID: SOC170-20220301 <span class="severity-high">High</span></h2>

<div class="section">
  <h3>1. Summary</h3>
  <p>An external IP (<strong>106.55.45.162</strong>) attempted a <strong>Local File Inclusion (LFI)</strong> attack on internal web server <strong>WebServer1006</strong> by requesting <code>/etc/passwd</code> via the URL. The server returned <strong>500 Internal Server Error</strong>, preventing file exposure.</p>
</div>

<div class="section">
  <h3>2. Source IP Details (External)</h3>
  <table>
    <tr><th>Field</th><th>Value</th></tr>
    <tr><td>IP Address</td><td>106.55.45.162</td></tr>
    <tr><td>Network</td><td>TencentCloud (China)</td></tr>
    <tr><td>ASN / Route</td><td>AS45090, 106.52.0.0/14</td></tr>
    <tr><td>Admin Contact</td><td>James Tian – johnsonqu@tencent.com</td></tr>
    <tr><td>Technical Contact</td><td>Jimmy Xiao – klayliang@tencent.com</td></tr>
    <tr><td>Abuse Contact</td><td>tencent_noc@tencent.com</td></tr>
    <tr><td>Reputation</td><td>⚠️ Possibly Malicious – SSH brute-force, web attacks</td></tr>
    <tr><td>IP Type</td><td>Public cloud / dynamic assignment possible</td></tr>
  </table>
</div>

<div class="section">
  <h3>3. Destination Device (Internal)</h3>
  <table>
    <tr><th>Field</th><th>Value</th></tr>
    <tr><td>IP Address</td><td>172.16.17.13</td></tr>
    <tr><td>Hostname</td><td>WebServer1006</td></tr>
    <tr><td>Device Owner</td><td>Unknown</td></tr>
    <tr><td>Last Logon</td><td>Not available</td></tr>
    <tr><td>Device Role</td><td>Web server</td></tr>
    <tr><td>Security Status</td><td>HTTP 500 prevents file access</td></tr>
    <tr><td>Firewall Action</td><td>Allowed</td></tr>
  </table>
</div>

<div class="section">
  <h3>4. Event Timeline</h3>
  <table>
    <tr><th>Time</th><th>Source</th><th>Destination</th><th>Event / Action</th><th>Status</th></tr>
    <tr><td>10:10 AM</td><td>106.55.45.162</td><td>172.16.17.13</td><td>LFI attempt (/etc/passwd)</td><td>🔴 High Risk</td></tr>
    <tr><td>10:10 AM</td><td>WebServer1006</td><td>106.55.45.162</td><td>HTTP 500 Response</td><td>🟡 Warning</td></tr>
  </table>
</div>

<div class="section">
  <h3>5. SOC Recommendations</h3>
  <ul>
    <li><strong>Immediate:</strong> Block the source IP at firewall, monitor for repeats, audit WebServer1006.</li>
    <li><strong>Investigation:</strong> Identify last logged-in user, review logs, check for similar patterns.</li>
    <li><strong>Proactive:</strong> Implement WAF rules, sanitize URL inputs, monitor IP reputation.</li>
  </ul>
</div>

<div class="section">
  <h3>6. Reporting & Escalation</h3>
  <table>
    <tr><th>Role</th><th>Contact</th></tr>
    <tr><td>Admin Contact</td><td>James Tian – johnsonqu@tencent.com</td></tr>
    <tr><td>Technical Contact</td><td>Jimmy Xiao – klayliang@tencent.com</td></tr>
    <tr><td>Abuse Contact</td><td>Tencent NOC – tencent_noc@tencent.com</td></tr>
  </table>
</div>

<div class="section">
  <h3>7. Color Legend</h3>
  <p class="legend">
    <span class="high"></span> High Risk 🔴 &nbsp;&nbsp;
    <span class="medium"></span> Warning 🟡 &nbsp;&nbsp;
    <span class="low"></span> Normal 🟢
  </p>
</div>

<div class="section">
  <h3>8. Conclusion</h3>
  <p>The attack represents a <strong>malicious LFI attempt</strong> from an external Tencent Cloud IP. While unsuccessful, it indicates probing activity. Immediate firewall mitigation, logging, and monitoring are recommended.</p>
</div>

</body>
</html>
