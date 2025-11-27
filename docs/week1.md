Week 1 — System Planning & Initial Setup
1. System Architecture Diagram

[architecture diagram.drawio](https://github.com/user-attachments/files/23810223/architecture.diagram.drawio)<mxfile host="app.diagrams.net" agent="Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36" version="29.2.1" pages="2">
  <diagram name="Page-1" id="aJiSIC7ti0S7uZeWaqJk">
    <mxGraphModel dx="1500" dy="519" grid="0" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="0" pageScale="1" pageWidth="827" pageHeight="1169" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <mxCell id="RECcu5rMeG-ZqxGRz19R-7" edge="1" parent="1" source="RECcu5rMeG-ZqxGRz19R-1" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;">
          <mxGeometry relative="1" as="geometry">
            <mxPoint x="206.33333333333337" y="113" as="targetPoint" />
          </mxGeometry>
        </mxCell>
        <mxCell id="RECcu5rMeG-ZqxGRz19R-1" parent="1" style="html=1;whiteSpace=wrap;" value="&lt;br&gt;&lt;div&gt;Host Computer&lt;/div&gt;&lt;div&gt;-------------------------------------------------------&lt;/div&gt;&lt;div&gt;&lt;br&gt;&lt;/div&gt;&lt;div&gt;(Windows, workstation)&lt;/div&gt;&lt;div&gt;-------------------------------------------------------&lt;/div&gt;&lt;div&gt;&lt;br&gt;&lt;/div&gt;&lt;div&gt;Powershell --&amp;gt; ssh client&lt;/div&gt;" vertex="1">
          <mxGeometry height="121" width="224.4" x="-239" y="43" as="geometry" />
        </mxCell>
        <mxCell id="RECcu5rMeG-ZqxGRz19R-2" parent="1" style="html=1;whiteSpace=wrap;" value="Ubuntu Server VM&lt;div&gt;----------------------------------------------------------&lt;br&gt;&lt;div&gt;&lt;br&gt;&lt;/div&gt;&lt;div&gt;enp0s: 192.168.56.3&lt;/div&gt;&lt;div&gt;----------------------------------------------------------&lt;/div&gt;&lt;div&gt;&lt;br&gt;&lt;/div&gt;&lt;div&gt;Headless Server&lt;/div&gt;&lt;div&gt;&lt;br&gt;&lt;/div&gt;&lt;/div&gt;" vertex="1">
          <mxGeometry height="123" width="236" x="205" y="42" as="geometry" />
        </mxCell>
        <mxCell id="RECcu5rMeG-ZqxGRz19R-9" edge="1" parent="1" style="endArrow=classic;html=1;rounded=0;entryX=1;entryY=1;entryDx=0;entryDy=0;" target="RECcu5rMeG-ZqxGRz19R-1" value="">
          <mxGeometry height="50" relative="1" width="50" as="geometry">
            <mxPoint x="203" y="163" as="sourcePoint" />
            <mxPoint x="148" y="94" as="targetPoint" />
          </mxGeometry>
        </mxCell>
        <mxCell id="RECcu5rMeG-ZqxGRz19R-11" edge="1" parent="1" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;">
          <mxGeometry relative="1" as="geometry">
            <Array as="points">
              <mxPoint x="170.33" y="66.57" />
              <mxPoint x="170.33" y="66.57" />
            </Array>
            <mxPoint x="74.33" y="66.57" as="sourcePoint" />
            <mxPoint x="204.99666666666664" y="66.57" as="targetPoint" />
          </mxGeometry>
        </mxCell>
        <mxCell id="RECcu5rMeG-ZqxGRz19R-10" parent="1" style="text;html=1;whiteSpace=wrap;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;rounded=0;" value="SSH (port 22)" vertex="1">
          <mxGeometry height="30" width="60" x="11" y="52" as="geometry" />
        </mxCell>
        <mxCell id="RECcu5rMeG-ZqxGRz19R-13" parent="1" style="text;html=1;whiteSpace=wrap;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;rounded=0;" value="Adapter 1:&amp;nbsp; NAT -&amp;gt; Internet Access" vertex="1">
          <mxGeometry height="30" width="238" x="-56" y="234" as="geometry" />
        </mxCell>
        <mxCell id="RECcu5rMeG-ZqxGRz19R-14" parent="1" style="text;html=1;whiteSpace=wrap;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;rounded=0;" value="Adapter 2 : Host-only (Vboxnet0)" vertex="1">
          <mxGeometry height="30" width="214" x="-15" y="184" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
  <diagram id="JC6ygJ_eXfPFMRbBMvBY" name="Page-2">
    <mxGraphModel dx="1185" dy="615" grid="0" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="0" pageScale="1" pageWidth="827" pageHeight="1169" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>



2. Distribution Selection Justification

Chosen server distribution: Ubuntu Server LTS
Alternative considered: Debian

Justification:

Ubuntu offers excellent documentation and strong community support.

Easy package management with apt.

Compatible with coursework tools.

Debian is more stable but slower with updates.

Ubuntu is better for beginners and aligns with industry practice.

3. Workstation Configuration Decision

Chosen workstation option: Option B — Host Machine

Reasons:

Windows PowerShell already includes SSH client.

No need to run another VM.

Lower resource usage.

Easier workflow (copy/paste, browser available).

Matches required “dual-system” architecture.

4. Network Configuration Documentation
VirtualBox Network Setup

Adapter 1 (NAT): Internet access

Adapter 2 (Host-Only Adapter – vboxnet0): Secure internal SSH network

(Insert screenshot of Adapter 1)
(Insert screenshot of Adapter 2)

Server Network Output

From ip addr command:

enp0s8 = 192.168.56.3/24 (Host-Only Network)

(Insert ip addr screenshot)

5. System Specifications (CLI Evidence)
Kernel Info (uname -a)

(Insert screenshot)

Memory Info (free -h)

(Insert screenshot)

Disk Info (df -h)

(Insert screenshot)

Network Info (ip addr)

(Insert screenshot)

Release Info (lsb_release -a)

(Insert screenshot)

6. Reflection

Example reflection you can copy:

This week I set up my Ubuntu Server VM and successfully connected to it using SSH from my host computer. I configured VirtualBox with both NAT and a Host-Only adapter and verified that the server received the correct IP address. I also collected system information using various Linux commands and created an architecture diagram. I initially encountered an issue where the host-only adapter was disabled and the VM did not receive an IP address, but fixing the adapter settings resolved the problem. Through this process I gained confidence in VirtualBox networking and remote administration.
