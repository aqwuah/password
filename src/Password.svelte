<script>
  import zxcvbn from 'zxcvbn';
  import prettyNum, {ROUNDING_MODE} from 'pretty-num';

  let password = "";
  let showPassword = false;
  let no_feedback, pretty_guesses, letters, warning, spec_characters, numbers, strength_text, protection, length, spaces, strength, crack_100ph_disp, crack_10ps_disp, crack_10kps_disp, crack_10bps_disp, crack_100ph_sec, crack_10ps_sec, crack_10kps_sec, crack_10bps_sec, guesses = 0
  let suggestions = [] 

  function validatePassword(e) {
    password = e.target.value;

    let result = zxcvbn(password);
    strength = result.score;
    length = password.length;
    letters = password.replace(/[^A-Za-z]/g,"").length;
    numbers = password.replace(/[^0-9]/g,"").length;
    spaces = (password.split(" ").length - 1);
    spec_characters = length-letters-numbers-spaces;
    warning = result.feedback.warning;
    suggestions.length = 0;
    suggestions = result.feedback.suggestions;

    if (warning != "") {
      if (warning.slice(-1) != ".") {
        warning = warning + ".";
      }
    }

    for (var i = 0; i < suggestions.length; i++) {
      if (suggestions[i].slice(-1) != ".") {
        suggestions[i] = suggestions[i]+".";
      }
    }

    if (warning == "" && suggestions.length == 0) {
      no_feedback = "There is no feedback for your password as it is secure enough."
    }

    if (strength == 0)
    {
      strength_text = "It is too guessable,"
      protection = "and provides no protection (it is a risky password)."
    }
    else if (strength == 1)
    {
      strength_text = "It is very guessable,"
      protection = "and provides protection only from throttled online attacks."
    }
    else if (strength == 2)
    {
      strength_text = "It is somewhat guessable,"
      protection = "but provides protection from throttled and unthrottled online attacks."
    }
    else if (strength == 3)
    {
      strength_text = "It is safely unguessable,"
      protection = "and provides moderate protection from offline slow-hash scenarios (+ strong protection from online attacks)."
    }
    else if (strength == 4)
    {
      strength_text = "It is very unguessable,"
      protection = "and provides strong protection from offline slow-hash scenarios (+ strong protection from online attacks)."
    }

    if (password.length !== 0)
    {
      crack_100ph_disp = result.crack_times_display.online_throttling_100_per_hour
      crack_10ps_disp = result.crack_times_display.online_no_throttling_10_per_second
      crack_10kps_disp = result.crack_times_display.offline_slow_hashing_1e4_per_second
      crack_10bps_disp = result.crack_times_display.offline_fast_hashing_1e10_per_second
      crack_100ph_sec = result.crack_times_seconds.online_throttling_100_per_hour
      crack_10ps_sec = result.crack_times_seconds.online_no_throttling_10_per_second
      crack_10kps_sec = result.crack_times_seconds.offline_slow_hashing_1e4_per_second
      crack_10bps_sec = result.crack_times_seconds.offline_fast_hashing_1e10_per_second
      guesses = prettyNum(result.guesses, {precision: 1, roundingMode: ROUNDING_MODE.HALF_UP});
      pretty_guesses = prettyNum(result.guesses, {thousandsSeparator: ","});
    }
    else
    {
      crack_100ph_disp = crack_10ps_disp = crack_10kps_disp = crack_10bps_disp = crack_100ph_sec = crack_10ps_sec = crack_10bps_sec = crack_10bps_sec = guesses = 0
    }
  }

  function hide (elements) {
  elements = elements.length ? elements : [elements];
  for (var index = 0; index < elements.length; index++) {
    elements[index].style.display = 'none';
  }
}

function show (elements) {
  elements = elements.length ? elements : [elements];
  for (var index = 0; index < elements.length; index++) {
    elements[index].style.display = 'block';
  }
}

  function strengthScore() {
    hide(document.querySelectorAll('.password-input'));
    show(document.querySelectorAll('.password-score'));

    var suggestionsContainer = document.getElementById("suggestionsList");
    suggestions.forEach(function(element, index){
      var elementForSuggestion = document.createElement('p');
      elementForSuggestion.innerText = element;
      suggestionsContainer.appendChild(elementForSuggestion);
    });
  }

  function back() {
    document.getElementById("input").value = "";
    if (suggestions.length != 0) {
      document.getElementById("suggestionsList").innerHTML = "";
    }
    strength = length =  letters = numbers = spaces = spec_characters = 0;
    crack_100ph_disp = crack_10ps_disp = crack_10kps_disp = crack_10bps_disp = crack_100ph_sec = crack_10ps_sec = crack_10bps_sec = crack_10bps_sec = guesses = 0
    hide(document.querySelectorAll('.password-score'));
    show(document.querySelectorAll('.password-input'));
  }
</script>

<style>
    form {
        --text-color: #afafaf;
    }

  .field {
    width: 100%;
    margin: 0 auto;
    position: relative;
    border-bottom: 2px dashed var(--text-color);
    margin: 4rem auto 1rem;
    transition: 500ms;
  }

  .label {
    color:var(--text-color);
    font-size: 1.2rem;
  }

  .input {
    outline: none;
    border: none;
    overflow: hidden;
    margin: 0;
    width: 100%;
    padding: 0.25rem 0;
    background: none;
    color: white;
    font-size: 1.2em;
    font-weight: bold;
    transition: border 500ms;
  }

  .input:valid {
    color: yellowgreen;
  }

  .input:invalid {
    color: orangered;
  }

  /* Border animation */

  .field::after {
    content: "";
    position: relative;
    display: block;
    height: 4px;
    width: 100%;
    background: #d16dff;
    transform: scaleX(0);
    transform-origin: 0%;
    opacity: 0;
    transition: all 500ms ease;
    top: 2px;
  }

  .field:focus-within {
    border-color: transparent;
  }

  .field:focus-within::after {
    transform: scaleX(1);
    opacity: 1;
  }

  /* Label animation */

  .label {
    z-index: -1;
    position: absolute;
    transform: translateY(-2rem);
    transform-origin: 0%;
    transition: transform 400ms;
  }

  .field:focus-within .label,
  .input:not(:placeholder-shown) + .label {
    transform: scale(0.8) translateY(-5rem);
    opacity: 1;
  }

  /* Strength Meter */

  .strength {
    display: flex;
    height: 20px;
    width: 100%;
  }

  .bar {
    margin-right: 5px;
    height: 100%;
    width: 25%;
    transition: box-shadow 500ms;
    box-shadow: inset 0px 20px #1f1f1f;
  }

  .bar-show {
    box-shadow: none;
  }

  .bar-1 {
    background: linear-gradient(to right, red, orangered);
  }

  .bar-2 {
    background: linear-gradient(to right, orangered, yellow);
  }

  .bar-3 {
    background: linear-gradient(to right, yellow, yellowgreen);
  }

  .bar-4 {
    background: linear-gradient(to right, yellowgreen, green);
  }

  .bar:last-child {
    margin-right: 0;
  }

  .strength-text {
    margin-top: 20px;
  }

  ul {
      list-style: none;
      margin: 10px 0;
      padding: 0;
      font-size: 0.7rem;
      text-align: left;
  }

  /* Buttons */

  button {
    margin-top: 2rem;
    padding: 10px 30px;
    font-weight: bold;
    border: 2px solid greenyellow;
    color: greenyellow;
    border-radius: 100px;
    background: transparent;
    transition: all 1000ms;
  }

  button:disabled {
    border-color: var(--text-color);
    color: var(--text-color);
  }

  .toggle-password {
    position: absolute;
    cursor: default;
    font-size: 0.8rem;
    right: 0.25rem;
    bottom: 0.5rem;
  }


</style>

<main>
  <form class="password-input" on:submit|preventDefault={strengthScore}>

    <div class="field">
      <input
        type={showPassword ? 'text' : 'password'}
        name="password"
        id="input"
        class="input"
        placeholder="
        "
        on:input={validatePassword}
        class:valid={strength > 3} />
      <label for="password" class="label">Password</label>
      <span
        class="toggle-password"
        on:mouseenter={() => (showPassword = true)}
        on:mouseleave={() => (showPassword = false)}
        on:pointerenter={() => (showPassword = true)}
        on:pointerleave={() => (showPassword = false)}>
        {showPassword ? '🙈' : '👁️'}
      </span>
    </div>
    <div class="strength">
      <span class="bar bar-1" class:bar-show={strength > 0} />
      <span class="bar bar-2" class:bar-show={strength > 1} />
      <span class="bar bar-3" class:bar-show={strength > 2} />
      <span class="bar bar-4" class:bar-show={strength > 3} />
    </div>

    <ul>
        <li><h2>Length: {length || "0"}</h2></li>
        <li>Letters: {letters || "0"}</li>
        <li>Numbers: {numbers || "0"}</li>
        <li>Spaces: {spaces || "0"}</li>
        <li>Special Characters: {spec_characters || "0"}</li>
    </ul>

    <div class="strength-text">
      <h2>Time to crack</h2>
      <h4>{guesses} guesses</h4>
      <ul>
        <li title={"Online attack on a service that ratelimits password auth attempts."}>Slow online: {crack_100ph_disp || "0"}</li>
        <li title={"Online attack on a service that doesn't ratelimit, or where an attacker has outsmarted ratelimiting."}>Fast online: {crack_10ps_disp || "0"}</li>
        <li title={"Offline attack with multiple attackers, proper salting, and a slow hash function with a moderate work factor."}>Slow offline: {crack_10kps_disp || "0"}</li>
        <li title={"Offline attack with multiple attackers, salting + fast hashing at about 10 billion/second."}>Fast offline: {crack_10bps_disp || "0"}</li>
      </ul>
    </div>

    <button disabled={strength == null || length == 0}>Strength Score</button>

  </form>

  <div class="password-score" style="display: none">
    <div class="password-text">
      <h2>Password</h2>
      <p on:mouseenter={() => (showPassword = true)} on:mouseleave={() => (showPassword = false)} on:pointerenter={() => (showPassword = true)} on:pointerleave={() => (showPassword = false)}>
        {showPassword ? password : '(hover/click to see)'}
      </p>
    </div>

    <div class="rating">
      <h2>Rating</h2>
      <p>Your password was rated <strong>{strength}</strong>/4.</p>
      <p>{strength_text} {protection}</p>
    </div>

    {#if warning == "" && suggestions.length == 0}
      <div class="no-feedback">
        <h2>Feedback</h2>
        <div class="no-feedback-box">
          <p>{no_feedback}</p>
        </div>
      </div>
    {/if}

    {#if warning != ""}
      <div class="warning">
        <h2>Warning</h2>
        <div class="warningList">
          <p>{warning}</p>
        </div>
      </div>
    {/if}

    {#if suggestions.length != 0}
      <div id="suggestions" class="suggestions">
        <h2>Feedback</h2>
        <div id="suggestionsList" class="suggestionsList">
        </div>
      </div>
    {/if}

    <div class="stats">
      <h2>Stats</h2>
      <p>Your password is <u>{length}</u> characters long.</p>
      <p>It contains {letters} {letters == 1 ? "letter" : "letters"}, {numbers} {numbers == 1 ? "number" : "numbers"}, {spec_characters} {spec_characters == 1 ? "special character" : "special characters"} and {spaces} {spaces == 1 ? "space" : "spaces"}.</p>
      <p>It would take approximately <u>{pretty_guesses}</u> guesses to crack your password.</p>
    </div>

    <div class="crackTimes">
      <h2>Crack Times</h2>
      <p>Online attack with a ratelimit: <u>{crack_100ph_disp || "0"}</u></p>
      <p>Online attack without a ratelimit: <u>{crack_10ps_disp || "0"}</u></p>
      <p>Offline attack with slow hashing (10K/s): <u>{crack_10kps_disp || "0"}</u></p>
      <p>Offline attack with fast hashing (10B/s): <u>{crack_10bps_disp || "0"}</u></p>
    </div>

    <div class="sequences">
      <h2>Sequences</h2>
      <p>(coming soon!)</p>
    </div>

    <button on:click={back}>Go back</button>
  </div>
</main>
