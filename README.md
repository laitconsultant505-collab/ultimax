<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ultimate Trip Ticket - Deployable Web Form</title>
    <!-- Bootstrap CSS (v5.3.8) -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-sRIl4kxILFvY47J16cr9ZwB07vP4J8+LH7qKQnuqkuIAvNWLzeN8tE5YBujZqJLB" crossorigin="anonymous">
    <style>
        body { padding: 20px; font-size: 1rem; }
        .signature-pad { border: 1px solid #ced4da; width: 100%; height: 150px; background: #f8f9fa; touch-action: manipulation; }
        .form-label { font-weight: bold; }
        @media (max-width: 576px) { /* Mobile phones */
            body { padding: 10px; font-size: 1.1rem; }
            .btn { padding: 0.75rem; font-size: 1.1rem; } /* Larger touch targets */
            .signature-pad { height: 120px; }
            .table td input { font-size: 1rem; }
        }
        @media (min-width: 577px) and (max-width: 1024px) { /* Tablets */
            body { padding: 15px; font-size: 1.05rem; }
            .signature-pad { height: 140px; }
        }
        .table-responsive { max-height: 300px; overflow-y: auto; } /* Scrollable tables on small screens */
    </style>
</head>
<body>
    <div class="container">
        <header class="mb-4">
            <h1 class="text-center">Ultimate Trip Ticket</h1>
        </header>
        <form id="tripForm" class="needs-validation" novalidate action="https://formspree.io/f/your-formspree-id" method="POST"> <!-- Replace 'your-formspree-id' with your actual Formspree endpoint -->
            <section class="mb-4 card">
                <div class="card-body">
                    <h2 class="card-title">Office Use Only</h2>
                    <div class="mb-3">
                        <label class="form-label">ATT/Accounts Coordinator Signature:</label>
                        <canvas id="officeSig" class="signature-pad" aria-label="Office Signature"></canvas>
                        <button type="button" class="btn btn-secondary mt-2" onclick="clearSig('officeSig')">Clear</button>
                        <input type="hidden" name="office_signature" id="officeSigData">
                    </div>
                    <div class="form-check">
                        <input type="checkbox" class="form-check-input" name="applicable_form" id="applicableForm">
                        <label class="form-check-label" for="applicableForm">Applicable Form for Email Supporting Correspondence</label>
                    </div>
                </div>
            </section>

            <section class="mb-4 card">
                <div class="card-body">
                    <h2 class="card-title">Client Details</h2>
                    <div class="row">
                        <div class="col-12 col-sm-6 mb-3">
                            <label class="form-label">Client Name:</label>
                            <input type="text" class="form-control" name="client_name" required>
                        </div>
                        <div class="col-12 col-sm-6 mb-3">
                            <label class="form-label">Dept/Sales:</label>
                            <input type="text" class="form-control" name="dept_sales">
                        </div>
                        <div class="col-12 col-sm-6 mb-3">
                            <label class="form-label">Booking Code:</label>
                            <input type="text" class="form-control" name="booking_code">
                        </div>
                        <div class="col-12 col-sm-6 mb-3">
                            <label class="form-label">Request Code:</label>
                            <input type="text" class="form-control" name="request_code">
                        </div>
                        <div class="col-12 col-sm-4 mb-3">
                            <label class="form-label">Name/Table:</label>
                            <input type="text" class="form-control" name="name_table">
                        </div>
                        <div class="col-12 col-sm-4 mb-3">
                            <label class="form-label">Cost Centre:</label>
                            <input type="text" class="form-control" name="cost_centre">
                        </div>
                        <div class="col-12 col-sm-4 mb-3">
                            <label class="form-label">Dept:</label>
                            <input type="text" class="form-control" name="dept">
                        </div>
                    </div>
                </div>
            </section>

            <section class="mb-4 card">
                <div class="card-body">
                    <h2 class="card-title">Trip Log</h2>
                    <div class="table-responsive">
                        <table class="table table-bordered" id="tripTable">
                            <thead>
                                <tr><th>Trip #</th><th>Time</th><th>Location</th></tr>
                            </thead>
                            <tbody>
                                <!-- Rows added dynamically -->
                            </tbody>
                        </table>
                    </div>
                    <div class="mb-3">
                        <label class="form-label">Total Trips:</label>
                        <input type="number" class="form-control" name="total_trips" readonly>
                    </div>
                </div>
            </section>

            <section class="mb-4 card">
                <div class="card-body">
                    <h2 class="card-title">Driver Certification</h2>
                    <p>I certify that the above trip(s) were completed as per the client's request.</p>
                    <div class="mb-3">
                        <label class="form-label">Signature:</label>
                        <canvas id="driverSig" class="signature-pad" aria-label="Driver Signature"></canvas>
                        <button type="button" class="btn btn-secondary mt-2" onclick="clearSig('driverSig')">Clear</button>
                        <input type="hidden" name="driver_signature" id="driverSigData">
                    </div>
                    <div class="mb-3">
                        <label class="form-label">Date:</label>
                        <input type="date" class="form-control" name="driver_date" required>
                    </div>
                </div>
            </section>

            <section class="mb-4 card">
                <div class="card-body">
                    <h2 class="card-title">Other Correspondence Pertaining to this Trip / Vehicle / Driver / Etc.</h2>
                    <div class="table-responsive">
                        <table class="table table-bordered">
                            <thead>
                                <tr><th>Date</th><th>Time</th><th>Location</th><th>Description</th></tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td><input type="date" class="form-control" name="corr_date1"></td>
                                    <td><input type="time" class="form-control" name="corr_time1"></td>
                                    <td><input type="text" class="form-control" name="corr_loc1"></td>
                                    <td><input type="text" class="form-control" name="corr_desc1"></td>
                                </tr>
                                <!-- Extend with more rows via JS if needed; one shown for base structure -->
                            </tbody>
                        </table>
                    </div>
                    <div class="mb-3">
                        <label class="form-label">Signature:</label>
                        <canvas id="corrSig" class="signature-pad" aria-label="Correspondence Signature"></canvas>
                        <button type="button" class="btn btn-secondary mt-2" onclick="clearSig('corrSig')">Clear</button>
                        <input type="hidden" name="corr_signature" id="corrSigData">
                    </div>
                    <div class="mb-3">
                        <label class="form-label">Date:</label>
                        <input type="date" class="form-control" name="corr_date">
                    </div>
                </div>
            </section>

            <section class="mb-4 card">
                <div class="card-body">
                    <h2 class="card-title">Client Confirmation</h2>
                    <p>I confirm that the above trip(s) were completed as per my request.</p>
                    <div class="mb-3">
                        <label class="form-label">Signature:</label>
                        <canvas id="clientSig" class="signature-pad" aria-label="Client Signature"></canvas>
                        <button type="button" class="btn btn-secondary mt-2" onclick="clearSig('clientSig')">Clear</button>
                        <input type="hidden" name="client_signature" id="clientSigData">
                    </div>
                    <div class="row">
                        <div class="col-12 col-sm-6 mb-3">
                            <label class="form-label">Name:</label>
                            <input type="text" class="form-control" name="client_name_confirm" required>
                        </div>
                        <div class="col-12 col-sm-6 mb-3">
                            <label class="form-label">Date:</label>
                            <input type="date" class="form-control" name="client_date" required>
                        </div>
                    </div>
                </div>
            </section>

            <section class="mb-4 card">
                <div class="card-body">
                    <h2 class="card-title">Other</h2>
                    <div class="mb-3">
                        <label class="form-label">PAX Names:</label>
                        <textarea class="form-control" name="pax_names" rows="3"></textarea>
                    </div>
                    <div class="form-check mb-3">
                        <input type="checkbox" class="form-check-input" name="no_tax" id="noTax">
                        <label class="form-check-label" for="noTax">NO TAX</label>
                    </div>
                    <div class="mb-3">
                        <label class="form-label">PAX:</label>
                        <input type="number" class="form-control" name="pax">
                    </div>
                    <div class="mb-3">
                        <label class="form-label">Billing Options:</label>
                        <div class="d-flex flex-wrap">
                            <div class="form-check me-3 mb-2">
                                <input type="radio" class="form-check-input" name="billing" value="Per Trip" id="perTrip">
                                <label class="form-check-label" for="perTrip">Per Trip</label>
                            </div>
                            <div class="form-check me-3 mb-2">
                                <input type="radio" class="form-check-input" name="billing" value="Non-Contract" id="nonContract">
                                <label class="form-check-label" for="nonContract">Non-Contract</label>
                            </div>
                            <div class="form-check me-3 mb-2">
                                <input type="radio" class="form-check-input" name="billing" value="Adhoc" id="adhoc">
                                <label class="form-check-label" for="adhoc">Adhoc</label>
                            </div>
                            <div class="form-check me-3 mb-2">
                                <input type="radio" class="form-check-input" name="billing" value="Other" id="other">
                                <label class="form-check-label" for="other">Other</label>
                            </div>
                            <div class="form-check me-3 mb-2">
                                <input type="radio" class="form-check-input" name="billing" value="Contract" id="contract">
                                <label class="form-check-label" for="contract">Contract</label>
                            </div>
                            <div class="form-check me-3 mb-2">
                                <input type="radio" class="form-check-input" name="billing" value="Per Day" id="perDay">
                                <label class="form-check-label" for="perDay">Per Day</label>
                            </div>
                            <div class="form-check me-3 mb-2">
                                <input type="radio" class="form-check-input" name="billing" value="Driver" id="driver">
                                <label class="form-check-label" for="driver">Driver</label>
                            </div>
                            <div class="form-check me-3 mb-2">
                                <input type="radio" class="form-check-input" name="billing" value="User" id="user">
                                <label class="form-check-label" for="user">User</label>
                            </div>
                            <div class="form-check me-3 mb-2">
                                <input type="radio" class="form-check-input" name="billing" value="Delivery Docket" id="deliveryDocket">
                                <label class="form-check-label" for="deliveryDocket">Delivery Docket (Uni-Doc-3911)</label>
                            </div>
                        </div>
                    </div>
                    <div class="mb-3">
                        <label class="form-label">Refer to Contract / SLA / Relay / Dock / Etc.:</label>
                        <textarea class="form-control" name="refer_to" rows="3"></textarea>
                    </div>
                </div>
            </section>

            <div class="text-center mb-4">
                <button type="submit" class="btn btn-primary btn-lg me-2">Submit Form via Email</button>
                <button type="button" class="btn btn-success btn-lg" onclick="downloadPDF()">Download PDF</button>
            </div>
        </form>
    </div>

    <!-- Bootstrap JS Bundle (v5.3.8) -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/js/bootstrap.bundle.min.js" integrity="sha384-FKyoEForCGlyvwx9Hj09JcYn3nv7wiPVlz7YYwJrWVcXK/BmnVDxM+D2scQbITxI" crossorigin="anonymous"></script>
    <!-- html2canvas (v1.4.1) -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <!-- jsPDF (v3.0.3) -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/3.0.3/jspdf.umd.min.js"></script>
    <script>
        // Initialize signature pads with unified pointer events for touch/mouse
        function initSig(canvasId) {
            const canvas = document.getElementById(canvasId);
            const ctx = canvas.getContext('2d');
            ctx.lineWidth = 2; ctx.strokeStyle = '#000';
            let drawing = false;
            const draw = (e) => {
                if (!drawing) return;
                ctx.lineTo(e.offsetX, e.offsetY);
                ctx.stroke();
            };
            canvas.addEventListener('pointerdown', (e) => { drawing = true; draw(e); });
            canvas.addEventListener('pointerup', () => drawing = false);
            canvas.addEventListener('pointermove', draw);
        }
        function clearSig(canvasId) {
            const canvas = document.getElementById(canvasId);
            canvas.getContext('2d').clearRect(0, 0, canvas.width, canvas.height);
        }
        initSig('officeSig');
        initSig('driverSig');
        initSig('corrSig');
        initSig('clientSig');

        // Dynamically add 16 trip rows
        const tbody = document.querySelector('#tripTable tbody');
        for (let i = 1; i <= 16; i++) {
            const row = document.createElement('tr');
            row.innerHTML = `
                <td>${i}</td>
                <td><input type="time" class="form-control" name="time${i}"></td>
                <td><input type="text" class="form-control" name="loc${i}"></td>
            `;
            tbody.appendChild(row);
        }

        // Form submission handler (validation, signatures, total trips)
        document.getElementById('tripForm').addEventListener('submit', function(e) {
            if (!this.checkValidity()) {
                e.preventDefault();
                this.classList.add('was-validated');
                return;
            }
            ['officeSig', 'driverSig', 'corrSig', 'clientSig'].forEach(id => {
                const dataId = id + 'Data';
                document.getElementById(dataId).value = document.getElementById(id).toDataURL('image/png');
            });
            let total = 0;
            for (let i = 1; i <= 16; i++) {
                const time = document.querySelector(`[name="time${i}"]`).value;
                const loc = document.querySelector(`[name="loc${i}"]`).value;
                if (time || loc) total++;
            }
            document.querySelector('[name="total_trips"]').value = total;
        });

        // PDF Download (captures full body for scrolled/mobile views)
        function downloadPDF() {
            const element = document.body;
            html2canvas(element, { 
                scale: window.devicePixelRatio, // High-DPI support
                useCORS: true,
                windowHeight: window.innerHeight,
                windowWidth: window.innerWidth
            }).then(canvas => {
                const imgData = canvas.toDataURL('image/png');
                const { jsPDF } = window.jspdf;
                const pdf = new jsPDF('p', 'mm', 'a4');
                const pdfWidth = pdf.internal.pageSize.getWidth();
                const pdfHeight = (canvas.height * pdfWidth) / canvas.width;
                pdf.addImage(imgData, 'PNG', 0, 0, pdfWidth, pdfHeight);
                pdf.save('ultimate-trip-ticket-filled.pdf');
            });
        }
    </script>
</body>
</html>
