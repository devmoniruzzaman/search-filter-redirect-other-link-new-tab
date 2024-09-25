<script>
jQuery(document).ready(function($) {
    // Define the URL mappings for each form and dropdown option
    var urlMap = {
        'gform_2': {
            'Detroit': 'https://food.google.com/chooseprovider?restaurantId=/g/11s2lxkn7x&g2lbs=AOHF13n-hP329_XA2DIZaWMu6ycSBDjAPHjCkbwx2nuBpdD3C8XeaEA6WiJEfYa-QwvR8UOG6Le7tTJYRQkfpKqy2vsCaPYYzGCFdl7Mm_g7dKFL0Ak6_ck%3D&hl=en-US&gl=us&cs=1&ssta=1&fo_m=MfohQo559jFvMUOzJVpjPL1YMfZ3bInYwBDuMfaXTPp5KXh-&gei=gu1EZoboLbCwptQPtPaG2AQ&ei=gu1EZoboLbCwptQPtPaG2AQ&opi=89978449&foub=mcpp&sa=X&ved=2ahUKEwiGsYGJlJCGAxUwmIkEHTS7AUsQjYwDKAB6BAgiEAI&addressId&orderType=2&partnerId=11344137403575542233&fulfillmentTime&menuSearchQuery&cartId&fo_s=OA&dineInLocationId&sei=CWd1c9xYaj29EZWnescl67o8&utm_campaign&utm_source=search',
            'Southfield': 'https://unclejoessf.hrpos.heartland.us/',
            'Warren': 'https://orderfood.google.com/chooseprovider?restaurantId=/g/1pyqprk_1&fo_m=MfohQo559jFvMWwP9igWZeWQMczq7voErUdXMU_hT8vrWuwRMUOzJVpjPL1Y&gei=P2xjYKrKJMmFtQaS0JmYDw&hl=en-US&fo_s=OA,AH&orderType=1&sa=X&ved=2ahUKEwjq5fWT0djvAhXJQs0KHRJoBvMQjYwDKAEwFnoECDMQBA&sei=CRwUG1rFntmlEZlz-vyoBwbV&utm_campaign&utm_source=search'
            // Add more mappings for form 1 as needed
        }
        // Add more forms and mappings as needed
    };

    // Handle custom button click event
    $('#custom-form-btn').on('click', function() {
        var $button = $(this); // Reference to the button
        var $form = $button.closest('form'); // Get the form related to the button
        var formId = $form.attr('id'); // Get the form ID
        var selectedValue = $form.find('select').val(); // Get the selected value from the dropdown



        // Check if the form ID and selected value are mapped
        if (urlMap[formId] && urlMap[formId][selectedValue]) {
            var redirectUrl = urlMap[formId][selectedValue];

            if (redirectUrl) {
                // Open the URL in a new tab immediately
                window.open(redirectUrl, '_blank');

                // Perform the AJAX request without delaying the action
                $.ajax({
                    url: $form.attr('action'),
                    type: 'POST',
                    data: $form.serialize(),
                    success: function() {
                        console.log('Form submission successful.');
                    },
                    error: function() {
                        console.error('Form submission failed.');
                    },
                    complete: function() {
                        // Re-enable the button after the process is complete
                        $button.prop('disabled', false).text('Start Order');
                    }
                });
            } else {
                // Re-enable the button if no URL is found
                $button.prop('disabled', false).text('Start Order');
            }
        } else {
            // Re-enable the button if no URL is found
            $button.prop('disabled', false).text('Start Order');
        }
    });
});


</script>
