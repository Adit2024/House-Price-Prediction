<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>House Price Prediction</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/css/bootstrap.min.css">
    <style>
        body {
            background-color: #f0f0f0;
        }
        .modal-dialog {
            max-width: 500px;
        }
    </style>
</head>
<body>
    <div class="container mt-5">
        <h1>House Price Prediction</h1>
        <form id="house-price-form">
            <div class="form-group">
                <label for="years">Years:</label>
                <input type="number" class="form-control" id="years" required>
            </div>
            <div class="form-group">
                <label for="area-type">Area Type:</label>
                <select class="form-control" id="area-type" required>
                    <option value="">Select Area Type</option>
                    <option value="luxury">Luxury</option>
                    <option value="affordable">Affordable</option>
                    <option value="semi-luxury">Semi-Luxury</option>
                </select>
            </div>
            <div class="form-group">
                <label for="location">Location:</label>
                <select class="form-control" id="location" required>
                    <option value="">Select Location</option>
                    <option value="central">Central Delhi</option>
                    <option value="north">North Delhi</option>
                    <option value="south">South Delhi</option>
                    <option value="east">East Delhi</option>
                    <option value="west">West Delhi</option>
                </select>
            </div>
            <div class="form-group">
                <label for="kitchen">Kitchen:</label>
                <select class="form-control" id="kitchen" required>
                    <option value="">Select Kitchen Type</option>
                    <option value="small">Small</option>
                    <option value="medium">Medium</option>
                    <option value="large">Large</option>
                </select>
            </div>
            <div class="form-group">
                <label for="bedroom">Bedroom:</label>
                <select class="form-control" id="bedroom" required>
                    <option value="">Select Bedroom Type</option>
                    <option value="1bhk">1 BHK</option>
                    <option value="2bhk">2 BHK</option>
                    <option value="3bhk">3 BHK</option>
                    <option value="4bhk">4 BHK</option>
                </select>
            </div>
            <div class="form-group">
                <label for="bathroom">Bathroom:</label>
                <select class="form-control" id="bathroom" required>
                    <option value="">Select Bathroom Type</option>
                    <option value="1">1 Bathroom</option>
                    <option value="2">2 Bathrooms</option>
                    <option value="3">3 Bathrooms</option>
                    <option value="4">4 Bathrooms</option>
                </select>
            </div>
            <button type="submit" class="btn btn-primary">Predict House Price</button>
        </form>
        <div class="modal fade" id="house-price-modal" tabindex="-1" role="dialog" aria-labelledby="housePriceModalLabel" aria-hidden="true">
            <div class="modal-dialog" role="document">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title" id="housePriceModalLabel">Predicted House Price</h5>
                        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                            <span aria-hidden="true">&times;</span>
                        </button>
                    </div>
                    <div class="modal-body">
                        <p id="predicted-house-price"></p>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/jquery@3.5.1/dist/jquery.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/js/bootstrap.bundle.min.js"></script>
    <script>
        $(document).ready(function() {
            $('#house-price-form').submit(function(e) {
                e.preventDefault();
                var years = $('#years').val();
                var areaType = $('#area-type').val();
                var location = $('#location').val();
                var kitchen = $('#kitchen').val();
                var bedroom = $('#bedroom').val();
                var bathroom = $('#bathroom').val();
                var basePrice = 10000000;
                var areaTypeMultiplier = getAreaTypeMultiplier(areaType);
                var locationMultiplier = getLocationMultiplier(location);
                var kitchenMultiplier = getKitchenMultiplier(kitchen);
                var bedroomMultiplier = getBedroomMultiplier(bedroom);
                var bathroomMultiplier = getBathroomMultiplier(bathroom);
                var housePrice = basePrice * (1 - (years / 100)) * areaTypeMultiplier * locationMultiplier * kitchenMultiplier * bedroomMultiplier * bathroomMultiplier;
                $('#predicted-house-price').text('The predicted house price is: ' + housePrice.toFixed(2));
                $('#house-price-modal').modal('show');
            });
            function getAreaTypeMultiplier(areaType) {
                switch (areaType) {
                    case 'luxury':
                        return 1.2;
                    case 'affordable':
                        return 0.8;
                    case 'semi-luxury':
                        return 1.0;
                    default:
                        return 1.0;
                }
            }
            function getLocationMultiplier(location) {
                switch (location) {
                    case 'central':
                        return 1.1;
                    case 'north':
                        return 0.9;
                    case 'south':
                        return 1.0;
                    case 'east':
                        return 0.8;
                    case 'west':
                        return 0.9;
                    default:
                        return 1.0;
                }
            }
            function getKitchenMultiplier(kitchen) {
                switch (kitchen) {
                    case 'small':
                        return 0.8;
                    case 'medium':
                        return 1.0;
                    case 'large':
                        return 1.2;
                    default:
                        return 1.0;
                }
            }
            function getBedroomMultiplier(bedroom) {
                switch (bedroom) {
                    case '1bhk':
                        return 0.6;
                    case '2bhk':
                        return 0.8;
                    case '3bhk':
                        return 1.0;
                    case '4bhk':
                        return 1.2;
                    default:
                        return 1.0;
                }
            }
            function getBathroomMultiplier(bathroom) {
                switch (bathroom) {
                    case '1':
                        return 0.6;
                    case '2':
                        return 0.8;
                    case '3':
                        return 1.0;
                    case '4':
                        return 1.2;
                    default:
                        return 1.0;
                }
            }
        });
    </script>
</body>
</html>
