#import matplotlib.pyplot as plt
from astropy.io import fits

# Load JWST NIRSpec spectrum
hdul = fits.open('jwst_nirspec_spectrum.fits')
data = hdul[1].data
wavelength = data['WAVELENGTH'] # in microns
flux = data['FLUX']
error = data['FLUX_ERR']

# Plot K2-18b transmission spectrum
plt.figure(figsize=(10,6))
plt.errorbar(wavelength, flux, yerr=error, fmt='o', alpha=0.6)
plt.axvline(1.4, color='red', linestyle='--', label='H2O 1.4um')
plt.axvline(3.3, color='blue', linestyle='--', label='CH4 3.3um')
plt.xlabel("Wavelength (micron)")
plt.ylabel("Transit Depth (ppm)")
plt.title("K2-18b JWST Transmission Spectrum")
plt.legend()
plt.savefig("k2-18b_spectrum.png")