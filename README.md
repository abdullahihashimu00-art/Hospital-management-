
        }

        function downloadPDF() {
            const btn = document.getElementById('pdfBtn');
            const loading = document.getElementById('loadingDiv');
            
            btn.disabled = true;
            loading.classList.add('show');
            
            const reports = document.querySelectorAll('.report-sheet');
            
            if (reports.length === 0) {
                alert('No reports to download!');
                btn.disabled = false;
                loading.classList.remove('show');
                return;
            }
            
            const pdfContent = document.createElement('div');
            pdfContent.style.width = '210mm';
            
            reports.forEach((report, index) => {
                const clone = report.cloneNode(true);
                clone.style.margin = '0';
                clone.style.pageBreakAfter = index < reports.length - 1 ? 'always' : 'auto';
                pdfContent.appendChild(clone);
            });
            
            const opt = {
                margin: 0,
                filename: 'Report_Sheets_' + new Date().toISOString().split('T')[0] + '.pdf',
                image: { type: 'jpeg', quality: 0.98 },
                html2canvas: { 
                    scale: 2,
                    useCORS: true,
                    logging: false