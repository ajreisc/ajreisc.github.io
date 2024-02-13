<!DOCTYPE html>
<html>
  <head>
    <script
      async
      src="https://cdn.fuseplatform.net/publift/tags/2/3025/fuse.js"
    ></script>
    <script>
      window.googletag = window.googletag || { cmd: [] };
      googletag.cmd.push(function () {
        googletag.pubads().set("page_url", "https://receiptify.herokuapp.com/");
        console.log("set");
      });
    </script>
    <script type="text/javascript">
      __tcfapi("addEventListener", 2, function (tcData, success) {
        console.log(`CMP event fired: ${JSON.stringify(tcData)}`);
      });
    </script>
    <!-- End Quantcast Choice. Consent Manager Tag v2.0 (for TCF 2.0) -->
    <!-- Global site tag (gtag.js) - Google Analytics -->
    <script
      async
      src="https://www.googletagmanager.com/gtag/js?id=UA-178665335-1"
    ></script>
    <script>
      window.dataLayer = window.dataLayer || [];
      function gtag() {
        dataLayer.push(arguments);
      }
      gtag("js", new Date());

      gtag("config", "UA-178665335-1");
    </script>
    <script type="text/javascript">
      (function () {
        function makeStub() {
          var TCF_LOCATOR_NAME = "__tcfapiLocator";
          var queue = [];
          var win = window;
          var cmpFrame;

          function addFrame() {
            var doc = win.document;
            var otherCMP = !!win.frames[TCF_LOCATOR_NAME];

            if (!otherCMP) {
              if (doc.body) {
                var iframe = doc.createElement("iframe");

                iframe.style.cssText = "display:none";
                iframe.name = TCF_LOCATOR_NAME;
                doc.body.appendChild(iframe);
              } else {
                setTimeout(addFrame, 5);
              }
            }
            return !otherCMP;
          }

          function tcfAPIHandler() {
            var gdprApplies;
            var args = arguments;

            if (!args.length) {
              return queue;
            } else if (args[0] === "setGdprApplies") {
              if (
                args.length > 3 &&
                args[2] === 2 &&
                typeof args[3] === "boolean"
              ) {
                gdprApplies = args[3];
                if (typeof args[2] === "function") {
                  args[2]("set", true);
                }
              }
            } else if (args[0] === "ping") {
              var retr = {
                gdprApplies: gdprApplies,
                cmpLoaded: false,
                cmpStatus: "stub",
              };

              if (typeof args[2] === "function") {
                args[2](retr);
              }
            } else {
              queue.push(args);
            }
          }

          function postMessageEventHandler(event) {
            var msgIsString = typeof event.data === "string";
            var json = {};

            try {
              if (msgIsString) {
                json = JSON.parse(event.data);
              } else {
                json = event.data;
              }
            } catch (ignore) {}

            var payload = json.__tcfapiCall;

            if (payload) {
              window.__tcfapi(
                payload.command,
                payload.version,
                function (retValue, success) {
                  var returnMsg = {
                    __tcfapiReturn: {
                      returnValue: retValue,
                      success: success,
                      callId: payload.callId,
                    },
                  };
                  if (msgIsString) {
                    returnMsg = JSON.stringify(returnMsg);
                  }
                  if (event && event.source && event.source.postMessage) {
                    event.source.postMessage(returnMsg, "*");
                  }
                },
                payload.parameter
              );
            }
          }

          while (win) {
            try {
              if (win.frames[TCF_LOCATOR_NAME]) {
                cmpFrame = win;
                break;
              }
            } catch (ignore) {}

            if (win === window.top) {
              break;
            }
            win = win.parent;
          }
          if (!cmpFrame) {
            addFrame();
            win.__tcfapi = tcfAPIHandler;
            win.addEventListener("message", postMessageEventHandler, false);
          }
        }

        makeStub();
      })();
    </script>
    <script type="text/javascript" src="ads.js"></script>
    <meta charset="UTF-8" />
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1.0, minimum-scale=0.5, user-scalable=yes"
    />
    <title>Receiptify</title>
    <link
      rel="stylesheet"
      href="//netdna.bootstrapcdn.com/bootstrap/3.1.1/css/bootstrap.min.css"
    />
    <link rel="stylesheet" href="styles.css" />
    <link
      rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/jqueryui/1.12.1/jquery-ui.css"
    />
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script src="https://code.jquery.com/ui/1.12.1/jquery-ui.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js"></script>
    <!-- Global site tag (gtag.js) - Google Analytics -->
  </head>
  <body onload="loadHome()">
    <div id="content"></div>
    <nav class="navColor">
      <div class="hamburger-menu">
        <span></span>
        <span></span>
        <span></span>
      </div>
      <ul>
        <li><a href="index.html">Home</a></li>
        <li><a href="about.html">About</a></li>
        <li><a href="privacy.html">Privacy Policy</a></li>
        <li><a href="contact.html">Contact</a></li>
        <li id="logout-btn">
          <button class="time-btn" id="logout">Log Out</button>
        </li>
      </ul>
    </nav>
    <div class="page-container">
      <div class="sticky-container">
        <div id="home_vrec_1"></div>
      </div>
      <div class="sticky-container sticky-container__right">
        <div id="home_vrec_2"></div>
      </div>
      <div class="content-container">
        <div class="container">
          <!-- <div class="temp sticky" id="home_vrec_1"></div> -->
          <div id="login">
            <div class="header-section">
              <div class="row">
                <div class="col-12">
                  <h1>Receiptify - Ari</h1>
                  <h2>Top Track Generator</h2>
                </div>
                <div class="row flex-center btns">
                  <div class="col-12 col-md-4">
                    <a href="/login" class="login-btn">Log in with Spotify</a>
                  </div>
                  <div class="col-12 col-md-4">
                    <a href="/lastfm" class="login-btn lastfm">Last.fm</a>
                  </div>
                  <!-- <div class="col-12 col-md-4">
                    <a href="/applemusic" class="login-btn apple"
                      >Log in with Apple Music*</a
                    >
                  </div> -->
                </div>
              </div>
            </div>
          </div>
          <div id="loggedin">
            <div class="main-body">
              <div class="receipt-wrapper">
                <div id="receipt"></div>
                <div id="start-searching">
                  Search for an album to view receipt
                </div>
              </div>
              <div class="customize">
                <div class="mobile-ad"><div id="home_header"></div></div>
                <p class="customize-header">Customize Receipt</p>
                <p>Metric</p>
                <form
                  class="form-group"
                  role="group"
                  aria-label="Top track type selection"
                  id="top-type"
                >
                  <select
                    class="form-select"
                    name="type-select"
                    id="type-select-dropdown"
                    autocomplete="off"
                  >
                    <option value="tracks" selected>Top Tracks</option>
                    <option value="artists">Top Artists</option>
                    <option value="genres">Top Genres</option>
                    <option value="stats">Stats</option>
                    <option value="show-search">Search Albums</option>
                    <option value="build-receipt">
                      Build Custom Receipt [NEW]
                    </option>
                  </select>
                </form>
                <p id="options-header">Time Period</p>
                <form
                  class="btn-group"
                  role="group"
                  aria-label="Time period selection"
                  id="options"
                >
                  <input
                    type="radio"
                    class="btn-check"
                    name="period-select"
                    id="short_term"
                    autocomplete="off"
                    checked
                    value="short_term"
                  />
                  <label class="btn btn-outline-secondary" for="short_term"
                    >Last Month</label
                  >
                  <input
                    type="radio"
                    class="btn-check"
                    name="period-select"
                    id="medium_term"
                    autocomplete="off"
                    value="medium_term"
                  />
                  <label class="btn btn-outline-secondary" for="medium_term"
                    >Last 6 Months</label
                  >

                  <input
                    type="radio"
                    class="btn-check"
                    name="period-select"
                    id="long_term"
                    autocomplete="off"
                    value="long_term"
                  />
                  <label class="btn btn-outline-secondary" for="long_term"
                    >All Time</label
                  >
                </form>
                <p id="num-header">Length</p>
                <form
                  class="btn-group"
                  role="group"
                  aria-label="Time period selection"
                  id="num-options"
                >
                  <input
                    type="radio"
                    class="btn-check"
                    name="num-select"
                    id="ten-tracks"
                    autocomplete="off"
                    checked
                    value="ten"
                  />
                  <label class="btn btn-outline-secondary" for="ten-tracks"
                    >Top 10</label
                  >
                  <input
                    type="radio"
                    class="btn-check"
                    name="num-select"
                    id="fifty-tracks"
                    autocomplete="off"
                    value="fifty"
                  />
                  <label for="fifty-tracks" class="btn btn-outline-secondary"
                    >Top 50</label
                  >
                </form>
                <p id="font-header">Font</p>
                <form
                  class="btn-group"
                  role="group"
                  aria-label="Font selection"
                  id="font-options"
                >
                  <input
                    type="radio"
                    class="btn-check"
                    name="font-select"
                    id="classic"
                    autocomplete="off"
                    checked
                    value="classic"
                  />
                  <label class="classic btn btn-outline-secondary" for="classic"
                    >CLASSIC</label
                  >
                  <input
                    type="radio"
                    class="btn-check"
                    name="font-select"
                    id="international"
                    autocomplete="off"
                    value="international"
                  />
                  <label
                    for="international"
                    class="international btn btn-outline-secondary"
                    >INTERNATIONALLY COMPATIBLE
                    <span class="new-feature">NEW</span></label
                  >
                </form>
                <form
                  class="btn-group"
                  role="group"
                  aria-label="Album search"
                  id="search-form"
                >
                  <input
                    type="text"
                    id="custom-name"
                    placeholder="Receipt title"
                  />
                  <input
                    type="text"
                    id="searchBox"
                    placeholder="Search for an album or track"
                  />
                  <div id="searchResult"></div>
                </form>
                <div id="explanation">
                  <p class="customize-header explanation-header">
                    Receipt Explained
                  </p>
                  <div id="definitions"></div>
                </div>
                <div id="track-edit">
                  <p class="customize-header explanation-header">Tracklist</p>
                </div>
              </div>
            </div>
          </div>
          <br />
        </div>
        <script id="user-profile-template" type="text/x-handlebars-template">
          <div class='receiptContainer {{#if isInternational}}anonymous{{/if}} {{#if isStats}}receiptContainerSmaller{{/if}}'>
            <h2 class='logo'>
              {{receiptTitle}}
            </h2>
            <p class='period'>
              {{period}}
            </p>
            <p class='date'>
              ORDER #000{{num}}
              FOR
              {{name}}
            </p>
            <p class='date'>
              {{time}}
            </p>
            <table class='tracks'>
              <thead>
                <td class='begin'>
                  QTY
                </td>
                <td>
                  ITEM
                </td>
                <td class='length'>
                  AMT
                </td>
              </thead>
              {{#each tracks}}
                <tr>
                  <td class='begin'>
                    {{this.id}}
                  </td>
                  <td class='name'>
                    {{#if this.url}}
                      <a
                        style='color: black; word-break: break-word'
                        href={{this.url}}
                        target='_blank'
                      >
                        {{{this.name}}}
                        {{{this.artists}}}
                      </a>
                    {{else}}
                      <p style='color: black; word-break: break-word; margin: 0px'>
                        {{{this.name}}}
                        {{{this.artists}}}
                      </p>
                    {{/if}}
                  </td>
                  <td class='length'>
                    {{this.duration_ms}}
                  </td>
                </tr>
              {{/each}}
              <tr class='total-counts'>
                <td class='begin' colspan='2'>
                  ITEM COUNT:
                </td>
                <td class='length'>
                  {{itemCount}}
                </td>
              </tr>
              <tr class='total-counts-end'>
                <td class='begin' colspan='2'>
                  TOTAL:
                </td>
                <td class='length'>
                  {{total}}
                </td>
              </tr>
            </table>
            <p class='date'>
              CARD #: **** **** **** 2023
            </p>
            <p class='date'>
              AUTH CODE: 123421
            </p>
            <p class='date'>
              CARDHOLDER:
              {{name}}
            </p>
            <div class='thanks'>
              <p>
                THANK YOU FOR VISITING!
              </p>
              <img src='barcode.png' />
              <p class='website'>
                receiptify.herokuapp.com
              </p>
              <img
                class='spotify-logo'
                id='spotify-logo'
                src='assets/img/Spotify_Logo_RGB_Black.png'
              />
            </div>
          </div>
          <div class='under'>
            <button class='time-btn' id='download'>Download Image</button>
            <button class='time-btn' id='new-tab'>View in New Tab <span class="new-feature">NEW</span></button>
            <button class='time-btn' id='save-playlist'>Save as Playlist <span class="new-feature">NEW</span></button>
          </div>
        </script>
        <!-- footer -->

        <div class="footer">
          <br />
          <br />
          <div class="desktop-ad"><div id="home_header"></div></div>
          <div class="seperator">
            <hr />
          </div>
          <br />
          <p class="info">
            Made by <a href="https://michellexliu.me/">Michelle Liu</a>
          </p>
          <p class="info">
            <a href="index.html">Home</a> | <a href="about.html">About</a> |
            <a href="privacy.html">Privacy Policy</a> |
            <a href="contact.html">Contact</a>
          </p>
          <br />
          <br />
        </div>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/handlebars.js/2.0.0-alpha.1/handlebars.min.js"></script>
        <script src="https://html2canvas.hertzen.com/dist/html2canvas.min.js"></script>
        <script src="dom-to-image.min.js"></script>
        <script src="FileSaver.min.js"></script>
        <script
          src="https://js-cdn.music.apple.com/musickit/v3/musickit.js"
          data-web-components
          async
        ></script>
        <script src="server.js"></script>
      </div>
    </div>
  </body>
</html>
