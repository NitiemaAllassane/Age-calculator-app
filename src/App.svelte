<script>

    let iconArrowImg = "/src/assets/images/icon-arrow.svg";

    let userDay = $state("");
    let userMonth = $state("");
    let userYear = $state("");

    let isDayError = $state(false);
    let dayErrorMessage = $state("");

    let isMonthError = $state(false);
    let monthErrorMessage = $state("");

    let isYearError = $state(false);
    let yearErrorMessage = $state("");

    let dayResult = $state();
    let monthResult = $state();
    let yearResult = $state();



    function validateField(name, value, min, max) {
        if (!value) {
            return { error: true, message: "This field is required" };
        }

        const num = parseInt(value);
        if (isNaN(num) || num < min || num > max) {
            return { error: true, message: `Must be a valid ${name}` };
        }

        return { error: false, message: "" };
    }


    function isValidDate(d, m, y) {
        const date = new Date(`${y}-${m}-${d}`);
        return (
            date.getFullYear() === y &&
            date.getMonth() + 1 === m &&
            date.getDate() === d
        );
    }



    // Handle form
    function handleFormSubmission(event) {
        event.preventDefault();

        isDayError = false;
        isMonthError = false;
        isYearError = false;
        dayErrorMessage = "";
        monthErrorMessage = "";
        yearErrorMessage = "";


        function validateAllFields() {
            const validations = [
                {
                    name: "day",
                    value: userDay,
                    min: 1,
                    max: 31,
                    setError: (err, msg) => {
                        isDayError = err;
                        dayErrorMessage = msg;
                    }
                },
                {
                    name: "month",
                    value: userMonth,
                    min: 1,
                    max: 12,
                    setError: (err, msg) => {
                        isMonthError = err;
                        monthErrorMessage = msg;
                    }
                },
                {
                    name: "year",
                    value: userYear,
                    min: 1000,
                    max: new Date().getFullYear(),
                    setError: (err, msg) => {
                        isYearError = err;
                        yearErrorMessage = msg;
                    }
                }
            ];

            let hasError = false;

            validations.forEach(({ name, value, min, max, setError }) => {
                const { error, message } = validateField(name, value, min, max);
                setError(error, message);
                if (error) hasError = true;
            });

            return !hasError;
        }



        const isValid = validateAllFields();
        if (!isValid) return;


        const day = parseInt(userDay);
        const month = parseInt(userMonth);
        const year = parseInt(userYear);
        const now = new Date();

        const birthDate = new Date(year, month - 1, day);
        const today = new Date();

        if (isNaN(birthDate.getTime()) || birthDate > today) {
            isDayError = true;
            dayErrorMessage = "Invalid date";
            return;
        }

        // Calcul d’âge
        let ageYear = today.getFullYear() - birthDate.getFullYear();
        let ageMonth = today.getMonth() - birthDate.getMonth();
        let ageDay = today.getDate() - birthDate.getDate();

        if (ageDay < 0) {
            ageMonth -= 1;
            const prevMonth = new Date(today.getFullYear(), today.getMonth(), 0);
            ageDay += prevMonth.getDate();
        }

        if (ageMonth < 0) {
            ageYear -= 1;
            ageMonth += 12;
        }

        yearResult = ageYear;
        monthResult = ageMonth;
        dayResult = ageDay;
    }
    
</script>



<main>
    <section class="calculator">
        <form onsubmit={handleFormSubmission}>
            <div class="inputs">
                <div class="period day">
                    <label for="day" class={{errorLab: isDayError}}>DAY</label>
                    <input type="number" name="day" id="day" placeholder="DD"  bind:value={userDay} class={{errorState: isDayError}} min="1" max="31" >
                    <div class="errorbox">
                        <p class="error day-error">{dayErrorMessage}</p>
                    </div>
                </div>
                <div class="period month">
                    <label for="month" class={{errorLab: isMonthError}}>MONTH</label>
                    <input type="number" name="month" id="month" placeholder="MM" bind:value={userMonth} class={{errorState: isMonthError}} min="1" max="12">
                    <div class="errorbox">
                        <p class="error month-error">{monthErrorMessage}</p>
                    </div>
                </div>
                <div class="period year">
                    <label for="year" class={{errorLab: isYearError}}>YEAR</label>
                    <input type="number" name="year" id="year" placeholder="YYYY" bind:value={userYear} class={{errorState: isYearError}}>
                    <div class="errorbox">
                        <p class="error year-error">{yearErrorMessage}</p>
                    </div>
                </div>
            </div>
            <div class="submit-section">
                <span class="line"></span>
                <button class="calculateBtn" aria-label="Calculate your age">
                    <img src={iconArrowImg} alt="" aria-hidden="true">
                </button>
            </div>
        </form>

        <article class="age-results">
            <h1>
                <span>{!yearResult ? "- -" : yearResult}</span>
                YEARS
            </h1>
            <h1>
                <span>{!monthResult ? "- -" : monthResult}</span>
                MONTHS
            </h1>
            <h1>
                <span>{!dayResult ? "- -" : dayResult}</span>
                DAYS
            </h1>
        </article>

    </section>
</main>



<style>
    main {
        display: flex;
        justify-content: center;
        align-items: center;
        min-height: 100vh;
    }

    /* form {
        margin-bottom: 2em;
    } */

    .calculator {
        width: 850px;
        background-color: var(--white);
        padding: 2em;
        border-radius: 20px 20px 140px 20px;
    }

    .inputs {
        display: flex;
        align-items: center;
        gap: 2em;
    }

    label {
        display: block;
        margin-bottom: 0.5em;
        font-size: 1em;
        font-weight: var(--weight-sm);
        color: var(--grey-500);
    }

    label.errorLab {
        color: var(--red-400);
        font-weight: var(--weight-md);
    }

    input {
        display: block;
        max-width: 100%;
        padding: 20px;
        border: 1px solid var(--grey-200);
        border-radius: 5px;
        color: var(--grey-500);
        font-weight: var(--weight-md);
        font-size: 1.5em;
        cursor: pointer;
    }

    input:hover {
        border-color: var(--purple-500);
    }

    input.errorState {
        border: 2px solid var(--red-400);
    }

    p {
        font-size: 1em;
        font-weight: var(--weight-sm);
        min-height: 1.5em;
        margin-top: 10px;
    }

    .error {
        color: var(--red-400);
        font-style: italic;
    }

    input:focus {
        outline: 2px solid var(--purple-500);
    }

    input:not([place-holder]) {
        color: var(--black);
    }

    .period {
        width: 25%;
    }

    .line {
        width: 90%;
        height: 1px;
        background-color: var(--grey-200);
    }

    .submit-section {
        display: flex;
        align-items: center;
    }

    .calculateBtn {
        width: 80px;
        height: 80px;
        border-radius: 50%;
        border: none;
        background-color: var(--purple-500);
        display: flex;
        justify-content: center;
        align-items: center;
        cursor: pointer;
        transition: background-color 0.3s ease;
    }

    .calculateBtn:hover {
        background-color: var(--black);
    }

    h1 {
        font-size: 4rem;
        color: var(--black);
        font-weight: var(--weight-lg);
        font-style: italic;
    }

    h1 span {
        color: var(--purple-500);
    }

    @media screen and (max-width: 48rem) {
        .calculator {
            max-width: 90%;
            padding: 1em;
        }
    }

    @media screen and (max-width: 40rem) {
        .inputs {
            gap: 1em;
        }

        .period {
            width: 30%;
        }

        input {
            padding: 15px;
            font-size: 1em;
        }

        h1 {
            font-size: 2.5em;
        }

        .line {
            width: 100%;
            position: relative;
        }

        .calculateBtn {
            position: absolute;
            width: 64px;
            height: 64px;
        }

        .submit-section {
            flex-direction: column;
            justify-content: center;
            margin: 2em 0 4em 0;
        }

        
    }

       @media screen and (max-width: 320px) {
        h1 {
            font-size: 2em;
        }
    }
</style>