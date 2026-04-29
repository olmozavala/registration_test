# Semi-Automatic Non-Rigid Registration

This Dash app registers `img2.npy` into the pixel space of a selected slice from `img1.nii.gz` using corresponding landmarks selected by the user.

If `img1.nii.gz` is not present, the app falls back to `img1.png` so the interface can still be tested. If `img2.npy` is not present, it falls back to `img2.png`, then to a placeholder image.

## Run

```bash
UV_PROJECT_ENVIRONMENT=/home/olmozavala/uv/envs/eoasweb uv run python app.py
```

Then open the local Dash URL shown in the terminal.

## Workflow

1. Select the desired fixed-image slice with the slice slider.
2. Rotate either image 90 degrees clockwise or flip it horizontally if its orientation needs adjustment.
3. Click matching landmarks in the same order on the selected `img1.nii.gz` slice and `img2.npy`.
4. Use the undo buttons if a point is misplaced.
5. Select at least three matching point pairs.
6. Click **Run registration**.
7. Click **Save registered 2D image** to write a PNG in `registered_outputs/`.

The app computes a thin-plate-spline inverse mapping from the selected fixed-slice coordinates into `img2.npy` coordinates, then resamples `img2` so the registered output has the same height and width as the selected NIfTI slice.
