id: who
content_class: flexbox vcenter

<img data-src="images/me.png" style="width: 150px; height: 150px;">
<h3>Szymon Nowak</h3>
<h3><a href="https://twitter.com/szimek">@szimek</a></h3>

---

class: nobackground
content_class: flexbox vcenter

<h1 style="font-size: 120px; margin-bottom: 40px; margin-top: 100px">What is</h1>
<h1 style="font-size: 200px; margin-bottom: 40px; color: rgb(40, 40, 40);">WebRTC</h1>
<h1 style="font-size: 120px; margin-bottom: 40px;">?</h1>

---

content_class:

<h1 style="font-size: 140px; margin-top: 100px">peer-to-peer</h1>

---

content_class:

<h1 style="font-size: 140px; margin-top: 100px">peer-to-peer</h1>
<h1 style="font-size: 200px; text-align: right; margin: 100px 150px;">audio</h1>

---

content_class:

<h1 style="font-size: 140px; margin-top: 100px">peer-to-peer</h1>
<h1 style="font-size: 200px; text-align: right; margin: 100px 150px;">video</h1>

---

content_class:

<h1 style="font-size: 140px; margin-top: 100px">peer-to-peer</h1>
<h1 style="font-size: 200px; text-align: right; margin: 100px 150px;">data</h1>

---

content_class: flexbox vcenter centered

<blockquote class="rectangle-thought-border">
<h1><em>plugin-free video calls</em></h1>
</blockquote>

---

content_class: flexbox vcenter centered

<blockquote class="rectangle-speech-border">
  <h3 style="font-size: 45px; color: #747474;"><em>WebRTC: Ready to Get Real?</em></h3>
</blockquote>

---

content_class: flexbox vcenter centered

<blockquote class="rectangle-speech-border">
  <h3 style="font-size: 45px; color: #747474;"><em>"How Will WebRTC Affect the Business VoIP Market?"</em></h3>
</blockquote>

---

content_class: flexbox vcenter centered

<blockquote class="rectangle-speech-border">
  <h3 style="font-size: 45px; color: #747474;"><em>"Will Mobile Help or Hinder WebRTC?"</em></h3>
</blockquote>

---

content_class: flexbox vcenter centered

<blockquote class="rectangle-speech-border">
  <h3 style="font-size: 45px; color: #747474;"><em>"More talk about how #WebRTC can disrupt the existing #Telecom infrastructure with #OTT comms."</em></h3>
</blockquote>

---

class: fullviewport
content_class: flexbox vcenter

<h1 style="font-size: 160px;"><em style="font-weight: 100">how I got into this</em></h1>

---

body_class: game
class: nobackground fullviewport
content_class: flexbox vcenter

---

content_class: flexbox vcenter centered

<h1 style="font-size: 170px; letter-spacing: 10px; text-transform: uppercase;">A brief</h1>
<h1 style="font-size: 170px; letter-spacing: -3px; text-transform: uppercase; margin-left: -15px;">history</h1>
<h1 style="font-size: 130px; letter-spacing: -3px; text-transform: uppercase; margin-left: -15px;"">of <span style="color: rgb(40, 40, 40);">WebRTC</span></h1>

---

content_class: flexbox vcenter

<h2>10/2011</h2>
<h2>First working draft of the spec</h2>
TODO: picture telco / war-room

---

content_class: flexbox vcenter

<h2>02/2013</h2>
<h2>first cross-browser video call</h2>
<a href="https://www.youtube.com/watch?v=aN0851GtND4">https://www.youtube.com/watch?v=aN0851GtND4</a>
TODO: picture youtube

---

content_class: flexbox vcenter

<h2>02/2014</h2>
<h2>cross-browser data transfers in stable versions</h2>
TODO: picture telco / war-room

---

content_class: flexbox vcenter

<h2>07/2014</h2>
<h2>Google Hangouts use <small>kind of</small> WebRTC on Chrome 36+</h2>
TODO: picture

---

content_class: flexbox vcenter

<h2>Audio / Video</h2>

---

content_class: flexbox vcenter

<h2>Customer support</h2>
TODO: background custom-support.png

---

content_class: flexbox vcenter

<h2>Amazon Mayday</h2>

---

class: screenshot nobackground
content_class: flexbox vcenter

<img data-src="images/slides/amazon-mayday.jpg" class="full" />

---

content_class: flexbox vcenter

<h2>No infrastructure needed <sup>&#42;</sup></h2>

---

content_class: flexbox vcenter

<h2>1click.io</h2>
<h2>recording</h2>
<h2>multiple participants</h2>
<h2>low bandwidth</h2>

---

content_class: flexbox vcenter

<h2>browser to browser</h2>

---

content_class: flexbox vcenter

<h2>browser to phone</h2>

---

content_class: flexbox vcenter

<h2>Demo</h2>

---

class: nobackground

<iframe src="https://webrtc-twilio.herokuapp.com/"></iframe>

---

title: Backend code
content_class: flexbox vcenter

<pre class="prettyprint highlight">
require "sinatra"
require "twilio-ruby"

get "/" do
  capability = Twilio::Util::Capability.new ENV["ACCOUNT_SID"], ENV["ACCOUNT_TOKEN"]
  capability.allow_client_outgoing ENV["APP_SID"]
  capability.allow_client_incoming "FEC14"
  token = capability.generate
  erb :index, locals: {token: token}
end

post "/voice" do
  content_type "text/xml"

  "&lt;Response>
    &lt;Dial callerId=\"#{ENV['CALLER_PHONE_NUMBER']}\">
      &lt;Number>#{params[:PhoneNumber]}&lt;/Number>
    &lt;/Dial>
  &lt;/Response>"
end
</pre>

---

title: Frontend code
content_class: flexbox vcenter

<pre class="prettyprint highlight">
Twilio.Device.setup("<%= token %>", {debug: true});

function call() {
    var params = {"PhoneNumber": $("#number").val()};
    Twilio.Device.connect(params);
}

function hangup() {
    Twilio.Device.disconnectAll();
}

function anykey() {
    var conn = Twilio.Device.activeConnection();
    if (conn) conn.sendDigits("1");
}
</pre>

---

content_class: flexbox vcenter

<h2>web component anyone?</h2>

---

content_class: flexbox vcenter

TODO: Add info about similar services from Google IO 2013 talk

---

content_class: flexbox vcenter

<h2>phone-to-browser</h2>

---

content_class: flexbox vcenter

<h2>Demo</h2>

---

content_class: flexbox vcenter

<iframe src="http://www.frisb.com/"></iframe>

---

content_class: flexbox vcenter

<h2><a href="https://appear.in"><img data-src="images/slides/appearin-page.png"></a></h2>

---

content_class: flexbox vcenter

<blockquote class="twitter-tweet" data-conversation="none" lang="en"><p>Nice! <a href="https://twitter.com/hashtag/FirefoxOS?src=hash">#FirefoxOS</a> keeps improving - here testing appear.in between an <a href="https://twitter.com/hashtag/iPhone?src=hash">#iPhone</a> and a FirefoxOS phone :) <a href="https://twitter.com/hashtag/webRTC?src=hash">#webRTC</a> FTW! <a href="http://t.co/ZOir8snL4y">pic.twitter.com/ZOir8snL4y</a></p>&mdash; appear.in (@appear_in) <a href="https://twitter.com/appear_in/statuses/501749867841327104">August 19, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

---

content_class: flexbox vcenter

<h2><a href="https://talky.io"><img data-src="images/slides/talky-logo.png"></a></h2>

---

content_class: flexbox vcenter

<h2><a href="https://otalk.im"><img data-src="images/slides/otalk-page.png"></a></h2>

---

content_class: flexbox vcenter

<h2><a href="https://www.youtube.com/watch?v=velmlLKmIA8">Henrik Joreteg - Making WebRTC awesome</a></h2>

---

content_class: flexbox vcenter

<h2>developers - no infrastrcture <sup>&#42;</sup></h2>
<h2>users - no third-party app accounts</h2>

 ---

content_class: flexbox vcenter

<h2><a href="http://www.gospeaky.com"><img data-src="images/slides/speaky-logo.png"></a></h2>

---

content_class: flexbox vcenter

TODO: rapt.fm

---

content_class: flexbox vcenter

TODO: be my eyes (?) simple app, big social impact

---

content_class: flexbox vcenter

<h2><a href="https://webrtc-translate.herokuapp.com">Another demo!</a></h2>

---

content_class: flexbox vcenter

<h2>WebSpeech API rant</h2>

---

content_class: flexbox vcenter

<h2>image recognition</h2>

---

content_class: flexbox vcenter

<h2>security monitoring</h2>
<h2>baby monitor</h2>

---

class: nobackground
content_class: flexbox vcenter

<h2><a href="http://webrtchacks.com/baby-motion-detector/"><img data-src="images/slides/baby-monitor.png"></a></h2>

---

content_class: flexbox vcenter

<h2>WebAudio API integration</h2>

<h2>determine volume</h2>
<h2>change pitch of your voice</h2>
<h2>mix and broadcast music</h2>

---

content_class: flexbox vcenter

<h2>high CPU / batter usage</h2>
<h2>offload image processing to a third party service</h2>

---

content_class: flexbox vcenter

<h2><a href="http://www.kurento.org/"><img data-src="images/slides/kurento-logo.png"></a></h2>
<h2><a href="http://www.kurento.org/">Kurento</a></h2>

---

content_class: flexbox vcenter

<h2>screensharing</h2>

---

content_class: flexbox vcenter

<h2>Google Chromecast</h2>
<img data-src="images/slides/chromecast.jpg" class="full">

---

content_class: flexbox vcenter

<h2>Chrome via extension</h2>
<h2>FIrefox Nightly via flag + allowed domain whitelist</h2>

---

content_class: flexbox vcenter

<a href="https://www.webrtc-experiment.com/Pluginfree-Screen-Sharing">https://www.webrtc-experiment.com/Pluginfree-Screen-Sharing</a>

---

content_class: flexbox vcenter

<h2>Live streaming</h2>
<h2>games?</h2>

---

content_class: flexbox vcenter

<h2>Live streaming</h2>
<h2>presentations?</h2>

---

content_class: flexbox vcenter

<h2>WebRTC doesn't scale</h2>
<h2>rebroadcasting / simulcast</h2>

---

content_class: flexbox vcenter

<h2>data channels</h2>

---

content_class: flexbox vcenter

<h2>low-latency networking</h2>

---

content_class: flexbox vcenter

<h2>multiplayer games</h2>

---

content_class: flexbox vcenter

<iframe width="560" height="315" data-src="//www.youtube.com/embed/nqihx_K-Y-o?rel=0" frameborder="0" allowfullscreen></iframe>
<a href="https://hacks.mozilla.org/2013/03/webrtc-data-channels-for-great-multiplayer">BananaBread</a>

---

content_class: flexbox vcenter

<h2><a href="https://www.cubeslam.com/tech"><img data-src="images/slides/cube-slam.png"></a></h2>

---

content_class: flexbox vcenter

<h2><a href="https://developer.valvesoftware.com/wiki/Source_Multiplayer_Networking">Source Multiplayer Networking by Valve</a></h2>

---

content_class: flexbox vcenter

<h2>File sharing</h2>

---

content_class: flexbox vcenter

<img data-src="images/slides/xkcd-file-transfer.png">

---

content_class: flexbox vcenter

<h2>Demo</h2>

---

content_class: flexbox vcenter

<a href="https://www.sharedrop.io">sharedrop.io</a>

---

content_class: flexbox vcenter

<a href="https://www.reep.io">reep.io</a>

---

content_class: flexbox vcenter

<a href="https://www.sharefest.me">sharefest.me</a>

---

content_class: flexbox vcenter

CDN augmentation

---

content_class: flexbox vcenter

<a href="https://peercdn.com">PeerCDN</a>

---

content_class: flexbox vcenter

<a href="https://swarmify.com">Swarmify</a>

---

content_class: flexbox vcenter

<h2>BitTorrent</h2>
<div class="build">
  <a href="https://github.com/feross/webtorrent">feross / webtorrent</a>
</div>

---

content_class: flexbox vcenter

<h2>BBS</h2>
<div class="build">
  <a href="https://github.com/tsujio/webrtc-bbs">tsujio / webrtc-bbs</a>
</div>

---

content_class: flexbox vcenter

<h2>Tor</h2>

---

content_class: flexbox vcenter

<h2>web server</h2>
<div class="build">
  <a href="http://www.peer-server.com">PeerServer</a>
</div>

---

content_class: flexbox vcenter

<h2>How does WebRTC work?</h2>

---

content_class: flexbox vcenter

<h1>Google I/O 2013</h1>
<h1><a href="https://www.youtube.com/watch?v=p2HzZkd2A40">Real-time communication with WebRTC</a></h1>
<h1>by Justin Uberti and Sam Dutton</h1>


---

content_class: flexbox vcenter

SDP
ICE
STUN
TURN
RTP
SCTP

Libraries:
SimpleWebRTC
PeerJS
...
code examples

---

content_class: flexbox vcenter

Browser support

---

content_class: flexbox vcenter

Object RTC

---

content_class: flexbox vcenter

Links

---

content_class: flexbox vcenter

THE END
