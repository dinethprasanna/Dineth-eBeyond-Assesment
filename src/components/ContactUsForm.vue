<script setup>
import { onMounted } from 'vue';
import $ from 'jquery';

onMounted(() => {
    $('#contactForm').on('submit', function (e) {
        let valid = true;
        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

        // Clear old errors
        $('.error-msg').text('');

        if (!$('#first-name').val()) {
            $('#first_name_error').text('First Name is required.');
            valid = false;
        }

        if (!$('#last-name').val()) {
            $('#last_name_error').text('Last Name is required.');
            valid = false;
        }

        const email = $('#email').val();
        if (!email) {
            $('#email_error').text('Email is required.');
            valid = false;
        } else if (!emailRegex.test(email)) {
            $('#email_error').text('Invalid email format.');
            valid = false;
        }

        if (!$('#message').val()) {
            $('#message_error').text('Message is required.');
            valid = false;
        }

        if (!$('#agree').is(':checked')) {
            $('#agree-error').text('You must agree to continue.');
            valid = false;
        }

        if (!valid) {
            e.preventDefault();
        }
        if (valid) {
            e.preventDefault();
            const formData = {
                firstname: $('input[name="first-name"]').val(),
                email: $('input[name="email"]').val(),
                telephone: $('input[name="telephone"]').val(),
                message: $('textarea[name="message"]').val(),
                agree: $('input[name="agree"]').is(':checked')
            };

            console.log(formData);
            alert(
                "Form Validation Success!\n\n" +
                "Name: " + formData.firstname + "\n" +
                "Email: " + formData.email + "\n" +
                "Telephone: " + formData.telephone + "\n" +
                "Message: " + formData.message + "\n" +
                "Agree to terms: " + (formData.agree ? "Yes" : "No")
            );
        }
    });
});

</script>

<template>
    <form class="w-full" id="contactForm">
        <div class="flex flex-wrap -mx-3 mb-6">
            <div class="w-full md:w-1/2 px-3 mb-6 md:mb-0">
                <label class="block uppercase tracking-wide text-[#b6b6b6] text-base  mb-2" for="first-name">
                    First Name *
                </label>
                <input
                    class="appearance-none block w-full bg-[#3c3c3c] text-[#b6b6b6] border rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white"
                    id="first-name" name="first-name" type="text" />
                <p id="first_name_error" class="text-red-500 text-xs italic error-msg"></p>
            </div>

            <div class="w-full md:w-1/2 px-3">
                <label class="block tracking-wide text-[#b6b6b6] text-base  mb-2" for="last-name">
                    Last Name *
                </label>
                <input
                    class="appearance-none block w-full bg-[#3c3c3c] text-[#b6b6b6] rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
                    id="last-name" type="text" />
                <p id="last_name_error" class="text-red-500 text-xs italic error-msg"></p>
            </div>
        </div>

        <div class="flex flex-wrap -mx-3 mb-6">
            <div class="w-full px-3">
                <label class="block tracking-wide text-[#b6b6b6] text-base  mb-2" for="email">
                    Email *
                </label>
                <input
                    class="appearance-none block w-full bg-[#3c3c3c] text-[#b6b6b6] rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
                    id="email" name="email" type="email" />
                <p id="email_error" class="text-red-500 text-xs italic error-msg"></p>
            </div>
        </div>

        <div class="flex flex-wrap -mx-3 mb-6">
            <div class="w-full px-3">
                <label class="block tracking-wide text-[#b6b6b6] text-base  mb-2" for="telephone">
                    Telephone
                </label>
                <input
                    class="appearance-none block w-full bg-[#3c3c3c] text-white rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
                    id="telephone" name="telephone" type="tel" />
            </div>
        </div>

        <div class="flex flex-wrap -mx-3 mb-6">
            <div class="w-full px-3">
                <label class="block tracking-wide text-[#b6b6b6] text-base  mb-2" for="message">
                    Message
                </label>
                <textarea name="message" id="message" rows="4"
                    class="block rounded py-3 px-4 mb-3 w-full resize-none text-sm text-white bg-[#3c3c3c] "></textarea>
                <p id="message_error" class="text-red-500 text-xs italic error-msg"></p>
            </div>
        </div>

        <p class="block tracking-wide text-[#b6b6b6] text-base mb-6">* required fields</p>

        <div class="flex flex-wrap -mx-3 mb-6 ml-2">
            <div class="inline-flex items-center cursor-pointer gap-2">
                <input type="checkbox" id="agree" class="peer hidden" />
                <span
                    class="-mr-8 w-5 h-5 inline-block border border-white bg-black peer-checked:bg-white peer-checked:border-white transition-all duration-200"></span>

            </div>
            <label for="agree" class=" block tracking-wide text-[#b6b6b6] text-base pl-8"> I agree to the <a href="#" target="_blank" class="underline">Terms & Conditions</a></label>
            <p id="agree-error" class="block w-full text-red-500 text-sm error-msg"></p>
        </div>

        <div class="flex justify-center md:justify-end">
            <button type="submit"
                class="bg-[#cc9500] hover:bg-amber-300 cursor-pointer w-[200px] rounded text-lg uppercase text-white py-2 px-4">Submit</button>
        </div>

    </form>
</template>