<script>
    
    
</script>



<main>
    <section class="calculator">
        <form>
            <div class="inputs">
                <div class="period day">
                    <label for="day" class="">DAY</label>
                    <input type="number" name="day" id="day" placeholder="DD" class="">
                    <div class="errorbox">
                        <p class="error day-error"></p>
                    </div>
                </div>
                <div class="period month">
                    <label for="month">MONTH</label>
                    <input type="number" name="month" id="month" placeholder="MM" class="">
                    <div class="errorbox">
                        <p class="error month-error"></p>
                    </div>
                </div>
                <div class="period year">
                    <label for="year">YEAR</label>
                    <input type="number" name="year" id="year" placeholder="YYYY" class="">
                    <div class="errorbox">
                        <p class="error year-error"></p>
                    </div>
                </div>
            </div>
            <div class="submit-section">
                <span class="line"></span>
                <button class="calculateBtn" aria-label="Calculate your age">
                    <img src="/assets/images/icon-arrow.svg" alt="" aria-hidden="true">
                </button>
            </div>
        </form>

        <article class="age-results">
            <h1>
                <span>- -</span>
                YEARS
            </h1>
            <h1>
                <span>- -</span>
                MONTHS
            </h1>
            <h1>
                <span>- -</span>
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
        width: 750px;
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

    label.error-lab {
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

    input.error-state {
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
        .calculator {max-width: 90%;}
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