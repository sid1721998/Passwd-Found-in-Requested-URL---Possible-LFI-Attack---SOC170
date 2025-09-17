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
  .severity-medium {
    color: #fff;
    background-color: #f1c40f;
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
  .analysis {
    background-color: #dff0d8;
    border-left: 5px solid #3c763d;
    padding: 15px;
    margin-bottom: 20px;
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
  <h3>2. Alert Details</h3>
  <table>
    <tr><th>Field</th><th>Value</th></tr>
    <tr><td>EventID</td><td>120</td></tr>
    <tr><td>Event Time</td><td>Mar 01, 2022, 10:10 AM</td></tr>
    <tr><td>Rule</td><td>SOC170 - Passwd Found in Requested URL - Possible LFI Attack</td></tr>
    <tr><td>Level</td><td>Security Analyst</td></tr>
    <tr><td>Hostname</td><td>WebServer1006</td></tr>
    <tr><td>Destination IP</td><td>172.16.17.13</td></tr>
    <tr><td>Source IP</td><td>106.55.45.162</td></tr>
    <tr><td>HTTP Method</td><td>GET</td></tr>
    <tr><td>Requested URL</td><td>https://172.16.17.13/?file=../../../../etc/passwd</td></tr>
    <tr><td>User-Agent</td><td>Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; .NET CLR 1.1.4322)</td></tr>
    <tr><td>Alert Trigger Reason</td><td>URL Contains passwd</td></tr>
    <tr><td>Device Action</td><td>Allowed</td></tr>
    <tr><td>HTTP Response Status</td><td>500 Internal Server Error</td></tr>
    <tr><td>HTTP Response Size</td><td>0</td></tr>
  </table>
</div>

<div class="section">
  <h3>3. Source IP Analysis</h3>
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
  <h3>4. Destination Device (Internal)</h3>
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
  <h3>5. Event Timeline</h3>
  <table>
    <tr><th>Time</th><th>Source</th><th>Destination</th><th>Event / Action</th><th>Status</th></tr>
    <tr><td>10:10 AM</td><td>106.55.45.162</td><td>172.16.17.13</td><td>LFI attempt (/etc/passwd)</td><td>🔴 High Risk</td></tr>
    <tr><td>10:10 AM</td><td>WebServer1006</td><td>106.55.45.162</td><td>HTTP 500 Response</td><td>🟡 Warning</td></tr>
  </table>
</div>

<div class="section">
  <h3>6. SOC Analysis</h3>
  <div class="analysis">
    <p>✅ <strong>True Positive Alert:</strong> The alert correctly identified a malicious attempt targeting the <code>/etc/passwd</code> file.</p>
    <p>⚠️ <strong>Attack Outcome:</strong> The attack was <strong>unsuccessful</strong>. The server returned a 500 error and did not expose any sensitive information.</p>
    <p>🛡 <strong>Containment:</strong> No containment required for WebServer1006.</p>
    <p>📈 <strong>Escalation:</strong> No Tier 2 SOC escalation required.</p>
    <p>🌐 <strong>Attack Source:</strong> External Internet IP originating from China.</p>
  </div>
</div>

<div class="section">
  <h3>7. SOC Recommendations</h3>
  <ul>
    <li>Block the source IP <strong>106.55.45.162</strong> at the firewall.</li>
    <li>Monitor for repeat attempts from Tencent Cloud IP ranges.</li>
    <li>Audit WebServer1006 for any signs of compromise.</li>
    <li>Ensure URL input validation and WAF rules are in place to prevent LFI attacks.</li>
    <li>Track IP reputation via VirusTotal, Cisco Talos, and AbuseIPDB.</li>
  </ul>
</div>

<div class="section">
  <h3>8. Reporting & Escalation Contacts</h3>
  <table>
    <tr><th>Role</th><th>Contact</th></tr>
    <tr><td>Admin Contact</td><td>James Tian – johnsonqu@tencent.com</td></tr>
    <tr><td>Technical Contact</td><td>Jimmy Xiao – klayliang@tencent.com</td></tr>
    <tr><td>Abuse Contact</td><td>Tencent NOC – tencent_noc@tencent.com</td></tr>
  </table>
</div>

<div class="section">
  <h3>9. Color Legend</h3>
  <p class="legend">
    <span class="high"></span> High Risk 🔴 &nbsp;&nbsp;
    <span class="medium"></span> Warning 🟡 &nbsp;&nbsp;
    <span class="low"></span> Normal 🟢
  </p>
</div>

<div class="section">
  <h3>10. Conclusion</h3>
  <p>This incident represents a <strong>malicious LFI attempt</strong> from an external Tencent Cloud IP. Although the attempt was unsuccessful, it confirms active probing. Immediate mitigation and monitoring are recommended to prevent future attacks.</p>
</div>

</body>
</html>
